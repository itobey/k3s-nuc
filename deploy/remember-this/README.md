# remember-this

Argo CD deployment for the Amor Fati reader at https://remember-this.nuc.one.
Uses the existing Traefik middleware and cluster certificate configuration.
Configure DNS like the other `*.nuc.one` apps.

## First deployment

1. Publish `ghcr.io/itobey/remember-this:0.1` using the app repository's
   **Publish Image** workflow, or change the Deployment to a published tag.
   The image must be publicly pullable. A private package needs an image pull
   secret in this namespace and an `imagePullSecrets` reference in the Deployment.
2. Prepare the data directory on the NUC and install your generated JSON:

   ```sh
   sudo install -d -o 10001 -g 10001 -m 0700 /media/enc/docker-volumes/remember-this
   sudo install -o 10001 -g 10001 -m 0600 /path/to/positives.json /media/enc/docker-volumes/remember-this/positives.json
   ```

   Keep personal data out of Git. The app fails startup without an existing valid
   JSON file. Both directory and file must be writable by UID/GID 10001;
   `fsGroup` does not change ownership of a hostPath directory.
3. Commit/push these manifests, then register the application if `deploy/argo`
   is not already reconciled by your Argo CD bootstrap:

   ```sh
   kubectl apply -f deploy/argo/remember-this.yaml
   ```

4. Sync `remember-this` in Argo CD. Like the other apps, it uses manual sync
   and `CreateNamespace=true`.

## Storage and updates

The static PV retains `/media/enc/docker-volumes/remember-this` when the claim
is removed. Explicit binding pairs it with `remember-this-pvc`. This follows
the repository's single-node NUC storage layout.

Keep one replica and the `Recreate` strategy. The reader atomically rewrites
`positives.json` and uses a directory lock: mount the whole writable directory,
never a single-file subPath, ConfigMap, or Secret. Back up this directory,
including shared viewed/blacklisted state. Stop the reader before replacing
or re-exporting data, and preserve ownership and permissions.

Readiness uses `/readyz` to validate data and write access; liveness uses
`/healthz`. Neither probe consumes a memory. To update, publish a new image
tag, update the Deployment, and sync Argo CD.

The ingress uses the existing redirect/websocket middleware and adds no
authentication. Use the cluster's private network/access controls for diary data.
