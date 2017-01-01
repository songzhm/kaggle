# kaggle
kaggle competitions

# Set up Kagglegym Docker Local Enviroment
1. install [Docker for Mac](https://docs.docker.com/engine/installation/mac/)
2. clone or download folder kagglegym-master from this repo. Note: the docker setup folder originally from [here](https://github.com/Giqles/kagglegym), however, I edited the Dockerfile a little bit to give the docker user kaggler sudo permission.
3. download twosigma data from [here](https://www.kaggle.com/c/two-sigma-financial-modeling/data)
4. when data is extracted, extract `train.h5` file to the `../gym/input` in the folder `kagglegym-master`
5. run `docker build -t kagglegym .`
6. (optional) extra step that will make spinning up the container super easy, put the following lines in `.bash_profile` file:
    * `cd ~`
    * `sudo nano .bash_profile`
    * copy & paste the following lines of code: 
    
    ```bash 
    kpython(){
        docker run --rm -it -v $(pwd):/wd kagglegym python "$@"
    }
    ikpython() {
        docker run --rm -it -v $(pwd):/wd kagglegym ipython
    }
    kjupyter() {
        docker run --rm -it -v $(pwd):/wd -p 8888:8888 kagglegym jupyter notebook --no-browser --ip="0.0.0.0" --notebook-dir=/wd
    }
    ```
7. (optional) if you want to install any additional python library (e.g `pyreadline` to do the autocomplete in jupyter notebook)
    * `docker run -it kagglegym bash`
    * using bash shell command line code to install pip and all other necessary libraries

## Reference:
[Tutorial 1](https://github.com/Giqles/kagglegym)
[Tutorial 2](http://blog.kaggle.com/2016/02/05/how-to-get-started-with-data-science-in-containers/)
