# Steps 
### Created an ec2 instance . 
### Created a extra volume of 5gb having the same availability zone as the ec2 instance . 
### Connect the ec2 instance
Swith to root user . 
Used the below command to see the attached volumes . 
```
lsblk

```
### Attached the new volume to the ec2 instance
Then again run the command 
```
lsblk

```
to check the volumes attached the ec2 instance. Now i findout that the extra volume is attached to the ec2 instance . 

### Formatted the volume
In linux all the devices can be found inside /dev directory . 
Used below command to format the volume . 
```
mkfs.ext4 /dev/xvdf

```
### Created a directory to mount the volume
```
mkdir test

```
Used the below command to mount the volume into test directory . 
```
mount /dev/xvdf /test

```
### Checked whether the volume is mounted or not?

Used the below command
```
mountpoint /test

```
### Created some rendom data inside the /test directory .

### Now unmounted the /test directory and detached the extra volume from the ec2 instance . 

To unmount the /test used the below command 
 ```
unmount /test

```
Then detached the volume from the ec2 instance . This scenario is comparable to detaching a pendrive from a PC or laptop . 

### Created another ec2 instance in the same availability zone as the Extra volume i created before

### Attached the extra volume to the new ec2 instance created .
Checked the new volume is attached or not by writing the below command
```
lsblk

```
Avoided using mkfs.ext4 for formating the volume as it will delete all the content present inside the volume . 
Used the below command to check the whether content is present inside the volume or not . 
```
file -s /dev/xvdf

```
After using the command i found out ext4 filesystem . 

### Mounted the volume to a directory 
First created a directory 
```
mkdir testdata

```
Then mounted the volume to the directory
```
mount /dev/xvdf /testdata

```
### Checked whether volume is persistent or not?
First moved into the directory /testdata
```
cd /testdata

```
Then checked whether files are present using ls command
```
ls

```
