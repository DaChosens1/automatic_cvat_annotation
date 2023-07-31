## Common Issues

I faced a couple issues, that typically could be fixed by rerunning the model function, rerunning cvat in docker, expanding resource limits in docker for its VM. I will list some of them here and how I fixed it. You can view more detailed information by inspecting the webpage and navigating to console.

- Cannot connect; Console: Bad Gateway
  - ```
    sudo docker exec -it cvat_server bash -ic 'python3 ~/manage.py migrate'
    chmod -R 777 wait-for-it.sh
    ```
- Cannot connect; Console: Health Warning, disk above limit 90%
  - Go to docker settings and increase disk hard drive storage
 
- Terminal; ERROR: failed to solve: process "/bin/sh -c pip3 install ultralytics==8.0.114 opencv-python==4.7.0.72 numpy==1.24.3" did not complete successfully
  - Go to docker settings and increase allocated RAM
 
- Detection Error: Could not detect (or something of the like)
  - Either is increase CPU cores allocation or needs restart
