# CardioNIfTI
Software tools for preprocessing of cardiac MR DICOM datasets and conversion to NIfTI.

# Overview 
The files in this repository are organised as follows:

[Code](code):
1) repeated_slices.py (optional) – it identifies repeated cine slices, finds the latest repeat and deletes older versions
2) auto_conversion – converts multi and single frame dicoms into NIfTIs. It also identifies the end-diastolic and end-systolic frames in this cine and saves these as separate files (“LVSA_img_ED.nii.gz” and “LVSA_img_ES.nii.gz”)
3) LVSA_structure.py (optional) – creates a new folder - “LVSA” – which contains copies of the 3 new NIfTI files

[Data](data):
Contains 3 sample datasets on which the functions of the code can be run.

To run the code in the [code](code) directory, we provide a [Docker](https://www.docker.com) image with all the necessary dependencies pre-compiled. 

## 1. Installation/Usage Guide for Docker Image
A Docker image is available on dockerhub https://hub.docker.com/r/gdoumou/auto_conversion. This image contains a base Ubuntu linux operating system image set up with all the libraries required to run the code.

## Install Docker
For Windows 10 Pro first install Docker. Windows 10 Home users will require Docker toolbox.
Ensure you have the C drive selected as a shared drive in Docker settings (or in VirtualBox on W10 Home).
To visualise the cines download ITKsnap.

1-	Download Auto conversion Docker image
In W10 open PowerShell from the Windows search box (Win + X then I), in macOS navigate Finder > Applications > Utilities > Terminal, or in Linux any terminal can be used. Then download the pre-compiled image:

docker pull gdoumou/auto_conversion:latest
#check the image is there
docker images
#should show auto_conversion on the list of images on your local system

2 - Run 4Dsegment Docker image
# Note the path to the folder on your desktop eg /c/Users/home/Desktop/4Dsegment and substitute <folder-path> within this command:
docker run -it --rm -v <folder-path>:/code/data gdoumou/auto_conversion
eg:
docker run -it --rm -v /Users/GDoumou/Desktop/data/:/code/data gdoumou/auto_conversion

#When it logs in:
export LD_LIBRARY_PATH=/lib64

#navigate to code/data and check that it has mounted your data into the data folder:
cd data
ls

#note: if in MAC type
find . -name '.DS_Store' -type f –delete

#navigate back to /code
cd ..

#check the content
ls

# run the python scripts 
1) repeated_slices.py (optional) 
2) auto_conversion 
3) LVSA_structure.py (optional)
example:
python auto_conversion.py

#when you finish type
exit

3 - Outputs from the pipeline
Once the pipeline is finished, under the root directory of each subject, you have three nifti files, i.e., LVSA.nii.gz, LVSA_img_ED.nii.gz and LVSA_img_ES.nii.gz





