# Docker-CDS
Docker-CDS are a set of containerized data science methods.

## Quick Start

To run the examples below you need to have [Docker
installed](https://docs.docker.com/get-docker/).

### Visualization techniques

This command pulls the `venustiano/cds:rvispack-0.1.0` image from
Docker Hub in case it is not present on the local host. Then, it
displays information about the containerized package and the available
visualization techniques. Finally, it removes the stopped container.

```bash
docker run --rm venustiano/cds:rvispack-0.1.0
```

To create visualizations using this image, you need a tabular data
file and a JSON object stored in the current working directory. The
supported file formats are defined by
[`fread`](https://rdrr.io/cran/data.table/man/fread.html) function
implemented in the `R data.table` package.

**Violin plots:**

Data

```bash
wget https://raw.githubusercontent.com/rijksuniversiteit-groningen/rvispack/master/tests/testthat/data/iris.csv
```

JSON object in `violin_params.json`

```json
{
	"filename": "iris.csv",
	"y_variable": "sepal_length"
}
```


#### Linux and MacOS

```bash
docker run --rm -v "$PWD":/app/data venustiano/cds:rvispack-0.1.0 c_violin violin_params.json
```

#### Windows powershell
```bash
docker run --rm -v ${PWD}:/app/data venustiano/cds:rvispack-0.1.0 c_violin violin_params.json
```

will produce a violin plot in the `Rplots.pdf` file.


![alt violin plot](./docs/source/pics/Rplots.pdf.png)

### Another example

```json
{
    "filename": "ggplotmpg.csv",
    "y_variable": "hwy",
    "x_variable": "class",
    "colour": "class",
    "fill": "class",
    "rotxlabs": 45,
    "boxplot": {
		"addboxplot": true,
	    "width": 0.1
    },
	"save":{
	  "save": true,
	  "width": 15,
	  "height": 10,
	  "device": "png"
	}
}
```

#### Download the data and the JSON object

```bash
wget https://raw.githubusercontent.com/rijksuniversiteit-groningen/rvispack/master/tests/testthat/data/ggplotmpg.csv
wget https://raw.githubusercontent.com/rijksuniversiteit-groningen/rvispack/master/tests/testthat/params/mpg_params.json
```

#### Create the visualization

```bash
docker run --rm -v "$PWD":/app/data venustiano/cds:rvispack-0.1.0 c_violin mpg_params.json
```

![alt mpgviolin](docs/source/pics/ggplotmpg.csv-violin-20221009_203930.png)
