### Docker and NFS Storage
If we want to use NFS Stoarge with Docker Container. We need to 1st create directory and change owner for NFS Share from <b>NFS Server</b>.- 
- <b>From NFS Server</b></br>
Create a Directory for NFS Share
####
    mkdir -p /nfs-share
    chown -R nobody:nogroup /nfs-share
####
If we have child directory, so then same procedure for share that directory. </br>
I have a directory in /nfs-share this directory already shared on NFS. Now i create another directory in /nfs-share/wordpress
####
    mkdir -p /nfs-share/wordpress
    chown -R nobody:nogroup /nfs-share/wordpress
####
Now, adding this new created directory path in /etc/exports files.
####
Now, adding this directory path in /etc/exports files:
####
    nano /etc/exports
####
    /nfs-share 192.168.0.0/24(rw,sync,no_subtree_check,no_root_squash)
    /nfs-share 192.168.0.0/24(rw,sync,no_root_squash)
    /nfs-share/docker/wordpress-data 192.168.0.0/24(rw,sync,no_root_squash)
    /nfs-share/docker/web 192.168.0.0/24(rw,sync,no_root_squash)
    /nfs-share/nfsdata 192.168.0.0/24(rw,sync,no_root_squash)
    /nfs-share/docker/wordpress-data/mysql 192.168.0.0/24(rw,sync,no_root_squash)
    /nfs-share *(rw,sync,no_subtree_check,no_root_squash)
    /nfs-share/docker/wpdata 192.168.0.0/24(rw,sync,no_root_squash)

####
- <b>Now, From Docker Host</b></br>

