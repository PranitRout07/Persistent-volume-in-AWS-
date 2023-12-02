# Steps 
### Created an ec2 instance . 


<img width="1280" alt="Screenshot 2023-12-02 184725" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/6f645888-a96d-44de-9395-3be9c4bbf625">


### Created a extra volume of 5gb having the same availability zone as the ec2 instance . 

<img width="1280" alt="Screenshot 2023-12-02 185018" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/d60449fd-421a-4f70-82da-d9c9dc550ef4">


### Connect the ec2 instance
Swith to root user . 
Used the below command to see the attached volumes . 
```
lsblk

```
<img width="1280" alt="Screenshot 2023-12-02 185146" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/3446c1fc-d2df-49d4-a65e-d7405b7d59f9">

### Attached the new volume to the ec2 instance

<img width="1279" alt="Screenshot 2023-12-02 185246" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/933ffb0a-bc14-44a3-bae9-777266eaf0c5">

Then again run the command 
```
lsblk

```
to check the volumes attached the ec2 instance. Now i findout that the extra volume is attached to the ec2 instance . 
<img width="1280" alt="Screenshot 2023-12-02 185357" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/c23dfa5a-aff1-4983-8104-e569e7b4fcff">


### Formatted the volume
In linux all the devices can be found inside /dev directory . 
Used below command to format the volume . 
```
mkfs.ext4 /dev/xvdf

```

<img width="1272" alt="Screenshot 2023-12-02 185513" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/cef73678-365b-41a1-a8fc-42ecd73dd96f">


### Created a directory to mount the volume
```
mkdir test

```
Used the below command to mount the volume into test directory . 
```
mount /dev/xvdf test/

```
<img width="1277" alt="Screenshot 2023-12-02 185635" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/61db239a-4cf7-4f29-be6e-1e9200be6821">


### Checked whether the volume is mounted or not?

Used the below command
```
mountpoint test/

```
<img width="1276" alt="Screenshot 2023-12-02 185737" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/cb137f2e-6692-44b7-a33c-e8a878dc0e7f">


### Created some rendom data inside the /test directory .

<img width="1279" alt="Screenshot 2023-12-02 185920" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/0532ede7-eadc-4ebf-8eeb-026cea607d44">


### Now unmounted the test/ directory and detached the extra volume from the ec2 instance . 
To unmount the /test used the below command 
 ```
umount /test

```
<img width="1276" alt="Screenshot 2023-12-02 190217" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/e5d4d124-b342-4969-926d-7fc376738d71">

Then detached the volume from the ec2 instance . This scenario is comparable to detaching a pendrive from a PC or laptop . 

<img width="1280" alt="Screenshot 2023-12-02 190300" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/5ecb313d-7631-448d-9585-10f1a562f818">

### Created another ec2 instance in the same availability zone as the Extra volume i created before

<img width="1280" alt="Screenshot 2023-12-02 190815" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/7fae3555-440e-4abb-bcf4-635758af30db">


### Attached the extra volume to the new ec2 instance created .
Checked the new volume is attached or not by writing the below command
```
lsblk

```
<img width="1279" alt="Screenshot 2023-12-02 191021" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/1d5594a8-17a4-45e8-8dfc-2192e85ad9fb">

Avoided using mkfs.ext4 for formating the volume as it will delete all the content present inside the volume . 
Used the below command to check the whether content is present inside the volume or not . 
```
file -s /dev/xvdf

```
<img width="1271" alt="Screenshot 2023-12-02 191132" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/703c60a8-5f59-4b09-a845-41e95df16aa3">

After using the command i found out ext4 filesystem . 

### Mounted the volume to a directory 
First created a directory 
```
mkdir testdata

```
Then mounted the volume to the directory
```
mount /dev/xvdf testdata/

```
<img width="1280" alt="Screenshot 2023-12-02 191259" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/2d4b8b85-83ed-44d2-af12-073de97a5d14">

### Checked whether volume is persistent or not?
First moved into the directory testdata/
```
cd testdata/

```
Then checked whether files are present using ls command
```
ls

```
<img width="1280" alt="Screenshot 2023-12-02 191503" src="https://github.com/PranitRout07/Persistent-volume-in-AWS-/assets/102309095/7932f9b8-4fbc-40af-bdcf-a54b71547ddf">

