# Template-Python-Singularity
## A template to build executable Singularity images for Python projects

### Objective

This repo contains a template to create a Python app that will run in an executable Singularity container. A Singularity container can typically be used in data science projects to provide transparency and support of reproducibility.

### Content

* `utils/` : utility scripts. The code in this directory is not included in the singularity container.
  * `build_image.sh` : a script to build a container image based on `singularity/recipe.txt`. The corresponding Singularity image is executable, and contains the scripts in `src/`. By default, the execution of the container image runs `src/model.py` (edit `recipe.txt` to change this behavior).
  * `test_container.sh` : a script to test if the execution of the container image works properly.
* `singularity/`: contains the singularity image built with `build_image.sh`
  * `singularity_test` : a directory where a singularity image is copied and tested.
* `src/`: the code that is included in the container.
* `data/` : input data
* `output/` : where code output is stored

### Instruction to build the singularity container from the recipe.txt

To create an executable singularity container (which contains the code in `/src`) from `singularity/recipe.txt`, run :

```bash
./utils/build_container.sh
```

This will create a container image `/singularity/container.sif`.
To test the executable singularity container image, run :

```bash
./utils/test_container.sh
```

This will output the results of `src/model.py` in `singularity/test_singularity/output`.

### Instructions to execute the image

The singularity container image container.sif is executable, you can execute it by running:

```bash
singularity run ./singularity/container.sif <Argument for input path>
```

Note: `<Argument for input path> ` is optional, default is ./


### Instructions to run a custom model in the same environment

By default, the script called model.py is executed upon execution of the image.
To run a specific Python script locally on synthetic data in the container environment, activate the singularity container in Terminal using:

```bash
singularity shell ./singularity/container.sif
```

This will allow you to have an environment (`Singularity>`) to run the model without installing any additional package.
In order to run the model, run the following command :

```bash
Singularity> python3 src/script.py <Argument for input path>
```

This command can also be used to run the singularity without accessing the singularity shell:

```bash
singularity exec container.sif python3 src/script.py <Argument for input path>
```

### License

This software is distributed under the GNU GENERAL PUBLIC LICENSE. Please refer to the file LICENCE.txt included for details.
