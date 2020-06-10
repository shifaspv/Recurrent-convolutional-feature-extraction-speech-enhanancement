# gruCNN-SE: A fully recurrent feature extraction for speech enhancement
This is a Tensorflow implementation of the ```gruCNN-SE``` architecture suggested in <a href="https://arxiv.org/submit/3217566/view"> this paper</a>, where we suggested a recurrent feature extraction approach to model speech recurrency at the feature extraction stage itself. 
This is advantageous as the recurrency is being deemed in the extracted features, contrasting to the other models  <a href="https://www.microsoft.com/en-us/research/uploads/prod/2018/02/ZhaoZararTashevLee_ICASSP_2018.pdf">[1]</a>, <a href="https://web.cse.ohio-state.edu/~wang.77/papers/Tan-Wang1.interspeech18.pdf">[2]</a> , where the recurrency being modelled independtly from the front-end feature extraction.

Few samples from the trained model are displayed <a href="https://www.csd.uoc.gr/~shifaspv/IEEE_Letter-demo">here</a>, along with the other models.

## Brief description of the model architecture
![1 1](https://user-images.githubusercontent.com/33422097/84161101-9708fc00-aa77-11ea-9b55-573f05b6bd81.jpg)
<br>
As can be seen in the figure, the ```gruCNN-SE``` is a feature domain enhancement model that takes the noisy spectra as the input and extracts features recurrenctly over time. To better understand the exact layer wise details please refer to our paper <a href="https://arxiv.org/submit/3217566/view">at here</a> .

## Implemented On
Python - 3.6.8 <br>
Tensorflow - 1.14.0 <br>

We required few more very common Python packages, check the ```required.txt``` file and install if you don't have.
## Data set
The model displayed on the paper was trained on the manually created data set with clean speech from <a href="https://datashare.is.ed.ac.uk/handle/10283/1942">here</a>. You may download the the clean and noisy speech from there, and extract them to ```./data/NSDTSEA``` directory. 

Then, generate the lists of wave files ID for training and tessting using the ```./data/generate_wave_id_list.py```, and confirm that the names matches to the ones in ```./config/config_params.json```

## Descriptions of the ```./config/config_params.json``` file variables
<table>
  <tr>
    <th>"Name"</th>
    <th>"Discription"</th>
  </tr>
  
  <tr>
    <th>train_id_list:</th>
      <td>list of training wave files ID</td>
  </tr>
    <tr>
    <th>valid_id_list:</th>
      <td>list of validation files ID</td>
  </tr>
  <tr>
    <th>num_gruCNN_layers</th>
    <td>numbering of gruCNN layers employed</td>
  </tr>
<tr>
    <th>fft_bin_size</th>
    <td>size of the FFT window</td>
  </tr>
  <tr>
    <th>num_input_frames</th>
      <td> number of input/output frames being recurrently modelled for training</td>
  </tr>
    <tr>
    <th>filter_size_gruCNN</th>
    <td>size of gruCNN kernals </td>
  </tr>
    <tr>
    <th>num_channel_gruCNN</th>
    <td>channels at each layer of gruCNN </td>
  </tr>
<tr>
    <th>Regarin</th>
      <td>The level to which wave files are RMS normalised </td>
  </tr>
</table>

The **train_id_list** and **valid_id_list** are generated by ```./data/generate_wave_id_list.py``` file.
## Training the model

Go to the ```./src``` folder and run the ```train.py``` or copy the command below to command line 

```
python train.py
```

Optionally, you can resume the training that could not have been completed, by passing the second argument ```model_id```

```
python train.py --model_id=saved_model_id
```

Trained models are saved to the ```./saved_models``` directory

## Testing the model

You may either use the already trained model which is in the ```./saved_models```, or could have your own trained model.

Go to the ```./src``` folder, and compile the ```generate.sh``` file with first argument as the ```model_id```. 

```
./generate.sh saved_model_id
```

A new folder named ```./outputs/saved_model_id``` will be created and saved the output sample.
User can manually edit the wave file ID inside the ```generate.sh```, to generate over multiple files.


