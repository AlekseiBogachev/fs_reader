# fs_reader
There is the reader for experimental data obtained using the measuring complex for DLTS. It can read csv-files and experimental data split into two files (the latter is the obsolete and awkward format), one of which contains the results of DLTS measurements, the other contains the results of temperature measurements. It puts the data to pandas.DataFrame, later it can write it to csv or hdf5 files. It's also posible to show a plot of the data and write this image to .svg or .jpg. The example of plot is shown below.
![plot example](example_data\example.svg)

There is one **DataReader** class in this repository. It has one attribute and implements several methods.

## Attributes
**data : pandas.DataFrame**
It's a DataFrame containing the experimental data. There are several columns containing all necessary information:  
*time* - date and time than the measurement was performed,  
*frequency_hz* - filling pulse frequency in hertz,  
*dlts_v* - value of DLTS-signal in volts,  
*temperature_k* - temperature in kelvin,  
*dlts_pf* - value of DLTS-signal in picofarads,  
*bs* - bridge sensitivity in picofarads,  
*ls* - selector sensitivity in millivolts,  
*f_pulse* - duration of filling pulse in microseconds,  
*u1* - level of filling pulse 1 in volts,  
*ur* - reverse bias in volts,  
*time_between_meas* - time between two measurements in seconds,  
*integral_time* - time constant of the integrating circuit in seconds,  
*specimen_name* - name of the specimen.

A part of this DataFrame is shown below:

|                time |  frequency_hz |  dlts_v |  temperature_k |   dlts_pf |  bs |  ls | f_pulse |   u1 |    ur | time_between_meas | integral_time |      specimen_name |
| ------------------- | ------------- | ------- | -------------- | --------- | --- | --- | ------- | ---- | ----- | ----------------- | ------------- | ------------------ |
| 2021-12-01 15:06:10 |     2500.0000 |  -2.182 |        293.206 | -0.002182 |   1 | 100 |      20 | -1.0 | -12.0 |               3.5 |           3.0 | КТ117№3_п1(база 2) |


##Methods
**read_from_d_t(d_file_name, t_file_name, encoding='cp1251')** reads data from text files with experimental data.  
**read_from_csv(fname, encoding=None)** reads data from csv-file created by an instance of the ExperimentalDataReader class.  
**read_from_hdf(fname, key=None)** reads data from a binary file in the HDF5 format.  
**set_specimen_name(specimen_name)** writes the specimen name to the **specimen_name** column of the self.data attribute.  
**set_bs(bs=np.nan)** writes the bridge sensitivity value to the **bs** column of the self.data attribute.  
**set_ls(ls=np.nan)** Write the selector sensitivity to the **ls** column of the self.data attribute.  
**set_f_pulse(f_pulse=np.nan)** writes the duration of the filling pulse to the corresponding column of the self.data attribute.  
**set_u1(u1=np.nan)** writes the level of filling pulse 1 to the **u1** column of the self.data attribute.  
**set_ur(ur=np.nan)** writes the value of the reverse bias to the **ur** column of the self.data attribute.  
**set_time_between_meas(time=np.nan)** writes the value of time between measurements to the **time_between_meas** column of the self.data attribute.
**set_integral_time(time=np.nan)** write the value of the time constant of the integrating circuit to the **specimen_name** column of the self.data attribute.
**compute_dlts_pf()** converts values of DLTS-signal in volts to values in picofarads and writes them to the **dlts_pf** column of the self.data attribute.
**to_csv(fname)** writes the self.data DataFrame to the csv-file.
**to_hdf(fname, key='data')** writes the self.data DataFrame to the binary file in the HDF5 format.
**get_plot()** makes a plot of the experimental data.
