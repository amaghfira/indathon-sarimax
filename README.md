# indathon-sarimax
Project IndaThon 2024 menggunakan model SARIMAX di Python

## A. Identitas Diri 
Project ini dibuat oleh: 
Nama          : Aulia Maghfira S.Tr.Stat
Satuan Kerja  : BPS Provinsi Kalimantan Timur

## B. Petunjuk Running Model 
### Input 
Data yang digunakan adalah jumlah_penumpang_transjakarta.csv yang berisi jumlah penumpang dari tahun 2015-2023 (bulanan). 

### Petunjuk running data 
Untuk melakukan running data, ikuti langkah berikut:
1. Download file sarima2 dan buka dengan jupyter notebook
2. Install package yang diperlukan
3. Read data jumlah_penumpang_transjakarta.csv
4. Jalankan kode sampai akhir

### Daftar Library/Package 
pandas, 
numpy,
matplotlib,
datetime,
pmdarima

### Fungsi SARIMAX
Fungsi berikut digunakan untuk mendapatkan model SARIMAX: 

def sarimax_forecast(SARIMAX_model, periods=24):
    # Forecast
    n_periods = periods

    forecast_df = pd.DataFrame({"month_index":pd.date_range(df.index[-1], periods = n_periods, freq='MS').month},
                    index = pd.date_range(df.index[-1]+ pd.DateOffset(months=1), periods = n_periods, freq='MS'))

    fitted, confint = SARIMAX_model.predict(n_periods=n_periods, 
                                            return_conf_int=True,
                                            exogenous=forecast_df[['month_index']])
    index_of_fc = pd.date_range(df.index[-1] + pd.DateOffset(months=1), periods = n_periods, freq='MS')

    # make series for plotting purpose
    fitted_series = pd.Series(fitted, index=index_of_fc)
    lower_series = pd.Series(confint[:, 0], index=index_of_fc)
    upper_series = pd.Series(confint[:, 1], index=index_of_fc)
    print(fitted_series)

    # accuracy 
    
    
    # Plot
    plt.figure(figsize=(15,7))
    plt.plot(df["jumlah_penumpang"], color='#1f76b4')
    plt.plot(fitted_series, color='darkgreen')
    plt.fill_between(lower_series.index, 
                    lower_series, 
                    upper_series, 
                    color='k', alpha=.15)

    plt.title("SARIMAX - Forecast Jumlah Penumpang Bis Transjakarta")
    plt.show()

sarimax_forecast(SARIMAX_model, periods=24)

### Execution Time 
data yang diolah berukuran 2kb dengan waktu pemrosesan kurang dari 3 menit.

### Source Code 
Silakan mengunduh dari repository ini untuk mencoba running data.
