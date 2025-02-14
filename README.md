# Execution environment image build with ansible collection
- Create ansible virtual env and install ansible, ansible-builder
```
$ virtualenv ansible_ee
$ source ansible-ee/bin/activate
$ pip install ansible
$ pip install ansible-builder
```
- Build image with ansible-builder
```
$ cd general-ee
$ vim requirements.yml		#Add ansible-collection if you need more collection 
$ ansible-builder build -t ansible-ee:latest
$ podman images				#Check builded image
$ podman run -it localhost/ansible-execution-env /bin/bash 	#To check xml module in image ( #ansible-doc xml )
$ podman tag {IMAGE ID} general-ee:latest		#Change name
$ podman save localhost/general-ee -o general-ee.tar		#Save image
```
- Upload image to OLAM server and load image
```
$ su -l awx -s /bin/bash                    #To change user
$ podman load -i /tmp/general-ee.tar		#Load image
```
- To add new OLAM Execution Environments with custom image, login to OLAM
- Go to Execution Environments and click Add
  ![image](https://github.com/user-attachments/assets/c8116439-2156-4431-ae30-71eb9f72def7)
- Add Name*, Image*, Pull* and save (Image name will be loaded image out name from podman load command)
![image](https://github.com/user-attachments/assets/b8779669-0e11-45f4-b38d-df3d96954841)

