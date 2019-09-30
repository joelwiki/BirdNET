# BirdNET Soundscape Analysis
By [Stefan Kahl](https://github.com/kahst), [Shyam Madhusudhana](https://www.birds.cornell.edu/brp/shyam-madhusudhana/), and [Holger Klinck](https://www.birds.cornell.edu/brp/holger-klinck/)

For more information regarding the project visit: https://birdnet.cornell.edu/

## Introduction
How can computers learn to recognize birds from sounds? The Cornell Lab of Ornithology and the Chemnitz University of Technology are trying to find an answer to this question. Our research is mainly focused on the detection and classification of avian sounds using machine learning – we want to assist experts and citizen scientist in their work of monitoring and protecting our birds.

This repository provides the basic BirdNET recognition system to detect avian vocalizations in soundscape recordings.

<b>If you have any questions or problems running the scripts, don't hesitate to contact us.</b>

Contact:  [Stefan Kahl](https://github.com/kahst), [Chemnitz University of Technology](https://www.tu-chemnitz.de/index.html.en), [Media Informatics](https://www.tu-chemnitz.de/informatik/Medieninformatik/index.php.en)

E-Mail: stefan.kahl@informatik.tu-chemnitz.de

This project is licensed under the terms of the MIT license.

## Installation
This is a Theano/Lasagne implementation in Python for the identification of hundreds of bird species based on their vocalizations. This code is tested using Ubuntu 18.04 LTS but should work with other distributions as well. Python 2 and 3 are supported.

1. Clone the repository:

```
git clone https://github.com/kahst/BirdNET.git
```

2. Install requirements:

```
cd BirdNET
pip install –r requirements.txt
```
<i>You might need to add the full path to the requirements.txt in case pip throws an error: </i>'pip install -r /path/to/requirements.txt'. <i>These versions of required packages are known to work: NumPy 1.14.5, SciPy 1.0.0, Librosa 0.7.0, Future 0.17.1</i>

3. Librosa required audio backend (FFMPEG):

```
sudo apt-get install ffmpeg
```

4. Download model snapshot (300 MB):

```
sh model/fetch_model.sh
```

5. Install Lasagne/Theano:

```
pip install -r https://raw.githubusercontent.com/Lasagne/Lasagne/master/requirements.txt
pip install https://github.com/Lasagne/Lasagne/archive/master.zip
```

6. Install BLAS:

```
sudo apt-get install libblas-dev liblapack-dev
```

<i>You might have to add 'sudo' in front of the 'pip' command when admin privileges are required.</i>

7. Install GPU support (optional, but significantly faster):

Before installing <i>libgpuarray</i>, you need to install [CUDA](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) and [cuDNN](https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html) first: 

```
git clone https://github.com/Theano/libgpuarray.git
cd libgpuarray

cd <dir>
mkdir Build
cd Build
cmake .. -DCMAKE_BUILD_TYPE=Release
make
make install
cd ..

python setup.py build
python setup.py install

sudo ldconfig
```

<i>Again, you might need to add 'sudo' before install commands if admin privileges are required.

Please refer to the [Theano](http://deeplearning.net/software/theano/install_ubuntu.html) and [libgpuarray](http://deeplearning.net/software/libgpuarray/installation.html#step-by-step-install) install instructions if you encounter errors during install or execution.</i>

## Usage
BirdNET is an artificial neural network that can detect bird vocalizations in field recordings. This implementation runs in CPU-mode and does not require specialized hardware (you can run the script in GPU mode if you have a CUDA-enabled GPU available). A number of optional settings can be provided when executing the analysis script. Here are some examples for basic usage:

Analyze all '.wav'-files in a directory:

```
python analyze.py --i example/
```

Analyze a single file with known recording location:

```
python analyze.py --i example/Soundscape_1.wav --lat 42.479 --lon -76.451
```

The input arguments include:

```
--i: Path to input file or directory.
--o: Path to output directory. If not specified, the input directory will be used.
--filetype: Filetype of soundscape recordings. Defaults to 'wav'.
--results: Output format of analysis results. Values in ['audacity', 'raven']. Defaults to 'raven'.
--lat: Recording location latitude. Set -1 to ignore.
--lon: Recording location longitude. Set -1 to ignore.
--week: Week of the year when the recordings were made. Values in [1, 48]. Set -1 to ignore.
--overlap: Overlap in seconds between extracted spectrograms. Values in [0.0, 2.9].
--sensitivity: Sigmoid sensitivity; Higher values result in lower sensitivity. Values in [0.25, 2.0]. Defaults to 1.0.
```

Output formats support Raven and Audacity, but both formats are text-based and machine-readable.

## Sponsors

This project is supported by Jake Holshuh (Cornell class of ’66). The Arthur Vining Davis Foundations also kindly support our efforts.

The European Union and the European Social Fund for Germany partially funded this research. This work was also partially funded by the German Federal Ministry of Education and Research in the program of Entrepreneurial Regions InnoProfileTransfer in the project group localizeIT (funding code 03IPT608X)