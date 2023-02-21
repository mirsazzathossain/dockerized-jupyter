# Dockerized Jupyter

![Dockerized Jupyter](https://repository-images.githubusercontent.com/604392328/b14e7ed1-3cf0-4bf1-a33c-ac04da99f3d0)

This repository provides a `docker-compose.yml` file, based on the [jupyter/minimal-notebook](https://hub.docker.com/r/jupyter/minimal-notebook/) image, which is a minimal Jupyter notebook server. With Docker, you can easily set up a Jupyter Notebook environment without worrying about dependencies or affecting your local machine. The environment is self-contained and can be easily destroyed when you're done. It comes with an installed conda environment and you can install additional packages as needed, creating new environments for different projects. Additionally, the container is configured to automatically save your notebooks to a directory on your local machine, allowing for easy access outside of the container. All the Conda environments are also saved locally, making it easy to restore them if anything happens to the container. This repository is a great starting point for anyone looking to explore Jupyter and Docker.

## Pre-requisites

- [Docker](https://docs.docker.com/install/): Make sure you have Docker installed on your machine. Download and install guide can be found [here](https://docs.docker.com/install/).
- [Docker Compose](https://docs.docker.com/compose/install/): Make sure Docker Compose is also installed on your local machine. Docker Compose is included with Docker Desktop for Windows and macOS, but Linux users may need to install it separately. You can download Docker Compose from the [official website](https://docs.docker.com/compose/install/).

## Installation

1. Clone this repository to your local machine:

   ```bash
   git clone https://github.com/mirsazzathossain/dockerized-jupyter.git
   # or
   git clone git@github.com:mirsazzathossain/dockerized-jupyter.git
   ```

2. Change directory to the cloned repository:

   ```bash
    cd dockerized-jupyter
   ```

3. Create a `.env` file for environment variables:

   ```bash
   touch .env
   ```

4. Add the following environment variables to the `.env` file:

   ```yaml
   JUPYTER_TOKEN=your-jupyter-token
   PASSWORD_HASH=your-password-hash
   NOTEBOOK_USER=your-notebook-user
   ```

   Set a random string for `JUPYTER_TOKEN` which will be used to access the Jupyter Notebook server. You can generate a `PASSWORD_HASH` using the following command:

   ```bash
   python -c "from notebook.auth import passwd; print(passwd(passphrase='your-password', algorithm='sha1'))"
   ```

   This will generate a `PASSWORD_HASH` for the password `your-password`. When you run the command, you will see an output similar to the following:

   ```bash
   sha1:your-password-hash
   ```

   Copy the `PASSWORD_HASH` and paste it in the `.env` file. Set a username for `NOTEBOOK_USER` which will be used as the username in the Jupyter Notebook server.

5. Build the Docker container:

   ```bash
   docker compose up -d
   ```

6. Navigate to `http://localhost:8888` or `https://<your-public-ip>:8888` in your browser. You will be prompted to enter the `JUPYTER_TOKEN` you set in the `.env` file. Once you enter the token, you will be able to access the Jupyter Notebook server.

## Modifying the Configuration

If you need to modify the configuration of the Docker container, you can do so by editing the `docker-compose.yml` file. However, keep in mind that any changes you make to this file will not take effect until you restart the Docker container.

## Using conda in Jupyter Lab

You can create a new conda environment using the following command in the Jupyter Notebook terminal:

```bash
conda create --name myenv python=3.x
```

You can activate the environment using the following command:

```bash
conda activate myenv
```

To install packages in the environment, use the following command:

```bash
conda install -c conda-forge <package-name>
```

To deactivate the environment, use the following command:

```bash
conda deactivate
```

## Using conda environments as kernels in Jupyter

You can use the conda environments as kernels in Jupyter. To do so, first activate the environment you want to use as a kernel. Then, run the following command to install `ipykernel`:

```bash
conda install -c anaconda ipykernel
```

Once the installation is complete, run the following command to register the environment as a kernel:

```bash
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```

Restart the Jupyter Notebook kernel and you will see the new kernel in the kernel list. You can now use the environment as a kernel in Jupyter.

## Saving and restoring conda environments

You can save the conda environment to a file using the following command:

```bash
conda env export > environments/myenv.yml
```

If any thigs happen to the container, the conda environments will be saved in the `environments` directory on your local machine. Once you have the container up and running again, all the environments will be restored automatically.

## Contributing

If you have any suggestions or improvements, feel free to open an issue or submit a pull request. If you find this repository useful, please consider giving it a star.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details. Feel free to use this code in your projects, but please don't copy-paste it. Try to understand what it does and write it yourself. This will help you learn and understand the code better. You can read my blog post titled ["Dockerize Your Data Science Workflow: A Step-by-Step Guide to Setting Up Jupyter Lab on Your Private Linux Machine"](https://www.mirsazzathossain.me/articles/dockerizing-jupyter-notebook) for more details. If you do use it, a mention would be appreciated, but is not required. Thanks! :heart: [↩](#dockerized-jupyter)
