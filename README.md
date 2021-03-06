# Visualisasi Informasi menggunakan chart.js


## General Info
Halo! Saya Reyhan Venyutzky nrp 05211840000031. Project ini merupakan tugas UTS kelas Visualisasi Informasi ITS. Inti dari project ini berhasil membuat visualisasi dari data menggunakan chart.js. Untuk pembagian chart, saya seharusnya membuat `floating bars` tapi setelah melakukan processing dataset, `mixed chart` lebih tepat untuk digunakan.

### Dataset
Dataset yang digunakan adalah data berisi kecelakaan pesawat dan dataset berasal dari website kaggle dengan link berikut <br>
https://www.kaggle.com/datasets/deepcontractor/aircraft-accidents-failures-hijacks-dataset
<br>

### Tahapan Pembagunan Visualisasi Data

#### Persiapan Dataset
Dari dataset tersebut dilakukan processing untuk memilih data yang ingin ditampilkan. Berikut merupakan data yang ingin divisualisasikan yaitu.<br>
![image](https://user-images.githubusercontent.com/54930670/162118955-b7dbf6b6-fb69-49ba-93d6-33e32f02cc3f.png)
<br>
### Persiapan Template HTML
```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <title>Mixed Chart</title>
</head>

<body>
  <div class="chart-container" style="position: relative; height:40vh; width:80vw; margin-left: 5vw;">
    <canvas id="myChart"></canvas>
  </div>
  <script>
    const myChart = new Chart(
      document.getElementById('myChart'),
      config
    );
  </script>
</body>

</html>
```


#### 1. Melakukan Konfigurasi Data <br>
langkah pertama yaitu membuat const data yang berisikan dataset yang digunakan.<br>
```
 const data = {
            labels: ['2011', '2012','2013','2014','2015','2016','2017','2018','2019','2020','2021'],
            datasets: [{
                type: 'bar',
                label: 'Total Kecelakaan',
                data: [187,169,208,225,220,205,192,224,237,180,148,],
                fill: 50,
                borderColor: 'rgb(153, 204, 255)',
                backgroundColor: 'rgb(153, 204, 255)',
                yAxisID: 'y'
            }, {
                type: 'line',
                label: 'Total Korban Jiwa',
                data: [713,689,355,1219,840,567,317,963,471,430,330,],
                borderColor: 'rgb(255, 99, 132)',
                backgroundColor: 'rgba(255, 99, 132)',
                yAxisID: 'y1'
            }]
        };
```
untuk data total kecelakaan diset `type : bar` dan untuk total korban jiwa diset `type: line`

#### 2. Melakukan Konfigurasi Charts <br>
```
const config = {
            data: data,
            options: {
            }
}
```
Langkah selanjutnya adalah membuat tampilan charts lebih interaktif <br>
##### Memberikan Title
Di dalam `options` tambahkan `plugins` array <br>
```
                 plugins: {
                    responsive: true,
                    // untuk title
                    title: {
                        display: true,
                        text: 'Kecelakaan Pesawat Selama Tahun 2011 -2021',
                        font: {
                            size: 25,
                            weight: 'bold'
                        },
                        padding: {
                            top: 10,
                            bottom: 30
                        }
                    },
```
##### Memberikan legend dengan posisi di atas chart
Di dalam `plugins` tambahkan code berikut <br>
```
legend: {
    display: true,
    position: 'top',
    }
},
```
#### Memberikan animasi delay chart tampil di awal
Di dalam `options` tambahkan `animation` array tapi sebelumnya menambakhan variable dengan nama `delayed` <br>
```
// variabel 
        let delayed;
        const config = {
            data: data,
```
Kemudian menambahkan kode berikut
```
onComplete: () => {
     delayed = true;
},
delay: (context) => {
     let delay = 0;
     if (context.type === 'data' && context.mode === 'default' && !delayed) {
           delay = context.dataIndex * 300 + context.datasetIndex * 100;
     }
      return delay;
}
```
#### Memberikan animasi Loop dan ubah warna ketika mouse dihover ke chart
```
animation: {
    // untuk animasi loop
    radius: {
         duration: 400,
         easing: 'linear',
         loop: (context) => context.active
    },
    hoverRadius: 10,
    hoverBackgroundColor: 'rgb(0, 128, 255)',
    interaction: {
          mode: 'nearest',
          intersect: false,
           axis: 'x'
     }
```

#### Memberikan nama y-axis dan x-axis
```
scales: {
                    x: {
                        display: true,
                        title: {
                            display: true,
                            text: 'Tahun',
                            font: {
                                size: 18,
                                weight: 'bold',
                                lineHeight: 1.2
                            },
                            padding: {
                                top: 20,
                                left: 0,
                                right: 0,
                                bottom: 0
                            }
                        }
                    },
                    y: {
                        beginAtZero: true,
                        type: 'linear',
                        display: true,
                        position: 'left',
                        title: {
                            display: true,
                            text: 'Total Korban Jiwa',
                            font: {
                                size: 15,
                                weight: 'bold',
                                lineHeight: 1.2
                            },
                            padding: {
                                top: 30,
                                left: 0,
                                right: 0,
                                bottom: 0
                            }
                        }
                    },
                    y1: {
                        beginAtZero: true,
                        type: 'linear',
                        position: 'right',
                        display: true,
                        title: {
                            display: true,
                            text: 'Total Kecelakaan',
                            font: {
                                size: 15,
                                weight: 'bold',
                                lineHeight: 1.2
                            },
                            padding: {
                                top: 30,
                                left: 0,
                                right: 0,
                                bottom: 0
                            },
                            grid: {
                                drawOnChartArea: false, // only want the grid lines for one axis to show up
                            }
                        }
                    },
                }
            }
        };
```

## Berikut Hasilnya <br>
![image](https://user-images.githubusercontent.com/54930670/162153905-efe4e576-196b-40fe-8441-3580f4b023f6.png)




                    



