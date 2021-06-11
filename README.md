# physionet-config
Configuration data for PhysioNet

## Initial setup of this git repository
On the server (e.g. `physionet-live`), log in as `pn` and run:

    git init --bare /physionet/physionet-config.git

The directories `/physionet/physionet-build/config` and `/data/log/pn` should exist already.

On your development machine, run:

    git remote add physionet-live ssh://pn@physionet-live//physionet/physionet-config.git
    git checkout -b production
    scp .git/HEAD pn@physionet-live:/physionet/physionet-config.git/
    scp deploy/post-receive pn@physionet-live:/physionet/physionet-config.git/hooks/
    git push physionet-live production

## Updating files
Pushing to the `production` branch on `physionet-live` will result in the files being unpacked into `/physionet/physionet-build/config`.  In most cases, you will subsequently need to log in and restart/reload services (e.g. `sudo systemctl reload emperor.uwsgi.service`) for changes to take effect.
