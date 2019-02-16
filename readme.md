# Running Jupyter Notebook Container

Go to your terminal, run `docker --version` to make sure that docker is running properly on your computer.

### Build Image

Navigate to the project folder and into the notebooks folder.  \n
E.g. C:/Users/user/Desktop/jupyter-test/notebooks  \n 
Run the following code to build the jupyter notebook image
```
docker build -t <image name> .
```
Note that "image name" can be any name as specified by the user  \n 
**.** : Tells docker to look for 'Dockerfile' and build the image in current dir

### Run Image
```
docker run --rm -it -p 8811:8888 -v //c/Users/user/Desktop/jupyter-test/notebooks:/home/jovyan/work -e JUPYTER_ENABLE_LAB=yes <image name>
```
For windows users, it is important that our absolute directory starts with //c/ \n
Some explnation on the commands:
- **--rm**: remove the container once we exit.
- **-it**: allows connection to container's stdin channel, so when user do a ctrl+C to exit the container, **--rm** will be executed.
- **-p**: port mapping from local's 8811 to container's 8888
- **-v**: stands for volume, to create a mapping from our proj directory to container's work directory (So that we will have our notebooks inside the container and it will be in sync with our local machine)
- **-e JUPYTER_ENABLE_LAB=yes**: Launch in jupyter lab

### Execute Notebook (One Time Execution)
Command to run all the cell in one notebook, processing a file in the "input" folder and storing it in the "output" folder
```
docker run --rm -it -p 8181:8888 -v //c/Users/user/Desktop/jupyter-test/notebooks:/home/jovyan/work -e JUPYTER_ENABLE_LAB=yes jupyter-test jupyter nbconvert --to notebook --inplace --execute ./work/jupyter-test-nb.ipynb
```
