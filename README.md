# Template-Python-Singularity
## A template to build executable Singularity images in Python projects

### Objective

This repo contains a template to create a Python app that will run in an executable Singularity image. A Singularity containers can typically be used in data science projects to provide transparency and support of reproducibility.

### Content

* `singularity/`: singularity container
  * singularity_test
* `utils/` : utility scripts (to make submissions, etc)

* `src/`: models
* `data/` : input data
* `output/` : where code output is stored

### Instruction to build the singularity container from the recipe.txt

To create an executable singularity container (which contains the code in /src), run :

```bash
./utils/build_container.sh
```

This will create a container container.sif in /singularity.
To test the executable singularity container, run :

```bash
./utils/test_container.sh
```

This will output the results in singularity/test_singularity/output.

### Instructions to run the model

The singularity container container.sif is executable, you can reproduce the results by running:

```bash
singularity run ./singularity/container.sif <Argument for input path>
```

Note: `<Argument for input path> ` is optional, default is ./


Note that container.sif should be in the same folder as /training and /test.
The prediction scores on test dataset are saved in `./output/scores.csv`.
### Instructions to run a custom model in the same environment

To run a model locally on synthetic data in the container environement, activate the singularity container in Terminal using:

```bash
singularity shell ./singularity/container.sif
```

This will allow you to have an environment (`Singularity>`) to run the model without installing any additional package.
In order to run the model, run the following command :

```bash
Singularity> python3 src/model.py <Argument for input path>
```

For example, on my computer, when my cwd is the DreamHF folder, I run :

```bash
Singularity> python3 src/model.py ./
```

This command can also be used to run the singularity without accessing the singularity shell:

```bash
singularity exec container.sif python3 src/model.py <Argument for input path>
```


### License

This software is distributed under the GNU GENERAL PUBLIC LICENSE. Please refer to the file LICENCE.txt included for details.
