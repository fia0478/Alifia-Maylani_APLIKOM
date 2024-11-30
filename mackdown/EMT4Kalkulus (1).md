# Kalkulus dengan EMT
Materi Kalkulus mencakup di antaranya:


* 
Fungsi (fungsi aljabar, trigonometri, eksponensial, logaritma,
* komposisi fungsi)

* 
Limit Fungsi,

* 
Turunan Fungsi,

* 
Integral Tak Tentu,

* 
Integral Tentu dan Aplikasinya,

* 
Barisan dan Deret (kekonvergenan barisan dan deret).


EMT (bersama Maxima) dapat digunakan untuk melakukan semua perhitungan
di dalam kalkulus, baik secara numerik maupun analitik (eksak).


## Mendefinisikan Fungsi

Terdapat beberapa cara mendefinisikan fungsi pada EMT, yakni:


* 
Menggunakan format nama_fungsi := rumus fungsi (untuk fungsi
* numerik),

* 
Menggunakan format nama_fungsi &amp;= rumus fungsi (untuk fungsi
* simbolik, namun dapat dihitung secara numerik),

* 
Menggunakan format nama_fungsi &amp;&amp;= rumus fungsi (untuk fungsi
* simbolik murni, tidak dapat dihitung langsung),

* 
Fungsi sebagai program EMT.


Setiap format harus diawali dengan perintah function (bukan sebagai
ekspresi).


Berikut adalah adalah beberapa contoh cara mendefinisikan fungsi:


$$f(x)=2x^2+e^{\sin(x)}.$$\>function f(x) := 2\*x^2+exp(sin(x)) // fungsi numerik

\>f(0), f(1), f(pi)


    1
    4.31977682472
    20.7392088022

\>f(a) // tidak dapat dihitung nilainya


    Variable or function a not found.
    Error in:
    f(a) // tidak dapat dihitung nilainya ...
       ^

\>plot2d("2\*x^2+exp(sin(x))"):


![images/EMT4Kalkulus%20(1)-002.png](images/EMT4Kalkulus%20(1)-002.png)

Silakan Anda plot kurva fungsi di atas!


Berikutnya kita definisikan fungsi:


$$g(x)=\frac{\sqrt{x^2-3x}}{x+1}.$$\>function g(x) := sqrt(x^2-3\*x)/(x+1)

\>g(3)


    0

\>g(0)


    0

dapat dilihat bahwa x=0 dan x=3 membuat nilai g(x)=0, artinya x=0 dan
x=3 adalah akar-akar dari persamaan pada pembilang di fungsi g(x).


\>g(1) // kompleks, tidak dapat dihitung oleh fungsi numerik


    Floating point error!
    Error in sqrt
    Try "trace errors" to inspect local variables after errors.
    g:
        useglobal; return sqrt(x^2-3*x)/(x+1) 
    Error in:
    g(1) // kompleks, tidak dapat dihitung oleh fungsi numerik ...
        ^

\>plot2d("sqrt(x^2-3\*x)/(x+1)"):


![images/EMT4Kalkulus%20(1)-004.png](images/EMT4Kalkulus%20(1)-004.png)

\>f(g(5)) // komposisi fungsi


    2.20920171961

\>g(f(5))


    0.950898070639

\>function h(x) := f(g(x)) // definisi komposisi fungsi 

\>h(5) // sama dengan f(g(5))


    2.20920171961

Silakan Anda plot kurva fungsi komposisi fungsi f dan g:


dan


bersama-sama kurva fungsi f dan g dalam satu bidang koordinat.


\>function f(x):= x^3+1

\>function g(x):= x^2+x;

\>f(g(5)) // komposisi fungsi


    27001

\>g(f(5))


    16002

\>function h(x) := f(g(x)) // definisi komposisi fungsi

\>h(5) // sama dengan f(g(5))


    27001

\>function u(x) := g(f(x))

\>plot2d(["h(x)", "u(x)"], -10,10,0,10):


![images/EMT4Kalkulus%20(1)-005.png](images/EMT4Kalkulus%20(1)-005.png)

\>f(0:10) // nilai-nilai f(0), f(1), f(2), ..., f(10)


    [1,  2,  9,  28,  65,  126,  217,  344,  513,  730,  1001]

\>fmap(0:10) // sama dengan f(0:10), berlaku untuk semua fungsi


    [1,  2,  9,  28,  65,  126,  217,  344,  513,  730,  1001]

\>gmap(200:210)


    [40200,  40602,  41006,  41412,  41820,  42230,  42642,  43056,  43472,
    43890,  44310]

Misalkan kita akan mendefinisikan fungsi


$$f(x) = \begin{cases} x^3 & x>0 \\ x^2 & x\le 0. \end{cases}$$Fungsi tersebut tidak dapat didefinisikan sebagai fungsi numerik
secara "inline" menggunakan format :=, melainkan didefinisikan sebagai
program. Perhatikan, kata "map" digunakan agar fungsi dapat menerima
vektor sebagai input, dan hasilnya berupa vektor. Jika tanpa kata
"map" fungsinya hanya dapat menerima input satu nilai.


\>function map f(x) ...


      if x>0 then return x^3
      else return x^2
      endif;
    endfunction
</pre>
\>f(1)


    1

\>f(-2)


    4

\>f(-5:5)


    [25,  16,  9,  4,  1,  0,  1,  8,  27,  64,  125]

\>aspect(1.5); plot2d("f(x)",-5,5):


![images/EMT4Kalkulus%20(1)-007.png](images/EMT4Kalkulus%20(1)-007.png)

\>function f(x) &= 2\*E^x // fungsi simbolik


    
                                        x
                                     2 E
    

\>$f(a) // nilai fungsi secara simbolik


$$2\,e^{a}$$\>f(E) // nilai fungsi berupa bilangan desimal


    30.308524483

\>$f(E), $float(%)


$$2\,e^{e}$$$$30.30852448295852$$\>function g(x) &= 3\*x+1


    
                                   3 x + 1
    

\>function h(x) &= f(g(x)) // komposisi fungsi


    
                                     3 x + 1
                                  2 E
    

\>plot2d("h(x)",-1,1):


![images/EMT4Kalkulus%20(1)-011.png](images/EMT4Kalkulus%20(1)-011.png)

# Latihan

Bukalah buku Kalkulus. Cari dan pilih beberapa (paling sedikit 5
fungsi berbeda tipe/bentuk/jenis) fungsi dari buku tersebut, kemudian
definisikan fungsi-fungsi tersebut dan komposisinya di EMT pada
baris-baris perintah berikut (jika perlu tambahkan lagi). Untuk setiap
fungsi, hitung beberapa nilainya, baik untuk satu nilai maupun vektor.
Gambar grafik fungsi-fungsi tersebut dan komposisi-komposisi 2 fungsi.


Juga, carilah fungsi beberapa (dua) variabel. Lakukan hal sama seperti
di atas.


                             NOMOR 1  

$$a(x) = x^5 + 4x^2 - 5x - 21$$\>function a(x) &= (x^5 + 4\*x^2 - 5\*x - 21) // fungsi simbolik


    
                              5      2
                             x  + 4 x  - 5 x - 21
    

\>function a(x) &= (x^5 + 4\*x^2 - 5\*x - 21) // fungsi simbolik


    
                              5      2
                             x  + 4 x  - 5 x - 21
    

\>a(4)


    1047

\>a(-3:2)


    [-213,  -27,  -13,  -21,  -21,  17]

\>aspect(3); plot2d("a(x)",-3,2):


![images/EMT4Kalkulus%20(1)-013.png](images/EMT4Kalkulus%20(1)-013.png)

                            NOMOR 2  

$$g(x)=\sqrt{x^2+81}$$\>function g(x) := (sqrt(x^2+81)) // fungsi numerik

\>g(9)


    12.7279220614

\>a(-3:3)


    [-213,  -27,  -13,  -21,  -21,  17,  243]

\>aspect(3); plot2d("g(x)",-3,3):


![images/EMT4Kalkulus%20(1)-015.png](images/EMT4Kalkulus%20(1)-015.png)

                                NOMOR 3  

$$d(x)= \frac{x^2 + 12}{2x}$$\>function d(x) := ((x^2+12)/(2\*x)) // fungsi numerik

\>d(2)


    4

\>d=(-2:2)


    [-2,  -1,  0,  1,  2]

\>aspect(3); plot2d("d(x)",-2,2):


![images/EMT4Kalkulus%20(1)-017.png](images/EMT4Kalkulus%20(1)-017.png)

                             NOMOR 4  

$$f(x)= \cos{x}$$$$g(x)= \sin{x}$$\>function f(x) &= (cos(x)) // fungsi numerik


    
                                    cos(x)
    

\>f(pi)


    -1

\>f(3\*pi)


    -1

\>function g(x) &= (sin(x)) // fungsi numerik


    
                                    sin(x)
    

\>g(pi)


    0

\>g(2\*pi)


    0

\>f(g(pi)) // komposisi fungsi


    1

\>g(f(pi))


    -0.841470984808

\>function h(x) &= f(g(pi))


    
                                      1
    

\>plot2d("h(x)",-4,4):


![images/EMT4Kalkulus%20(1)-020.png](images/EMT4Kalkulus%20(1)-020.png)

Nomor 5


$$e(x) = \begin{cases} x-3 & x<2 \\ 1-x & x\ge2. \end{cases}$$\>function map e(x) ...


    if x<2 then return x-3
    else retrune 1-x
    endif;e(5)
    endfunction
</pre>
\>e(1)


    -2

\>e=(-3:3)


    [-3,  -2,  -1,  0,  1,  2,  3]

\>aspect(2); plot2d("e(x)",-2,1):


![images/EMT4Kalkulus%20(1)-022.png](images/EMT4Kalkulus%20(1)-022.png)

# Menghitung Limit

Perhitungan limit pada EMT dapat dilakukan dengan menggunakan fungsi
Maxima, yakni "limit". Fungsi "limit" dapat digunakan untuk menghitung
limit fungsi dalam bentuk ekspresi maupun fungsi yang sudah
didefinisikan sebelumnya. Nilai limit dapat dihitung pada sebarang
nilai atau pada tak hingga (-inf, minf, dan inf). Limit kiri dan limit
kanan juga dapat dihitung, dengan cara memberi opsi "plus" atau
"minus". Hasil limit dapat berupa nilai, "und" (tak definisi), "ind"
(tak tentu namun terbatas), "infinity" (kompleks tak hingga).


Perhatikan beberapa contoh berikut. Perhatikan cara menampilkan
perhitungan secara lengkap, tidak hanya menampilkan hasilnya saja.


\>$showev('limit(sqrt(x^2-3\*x)/(x+1),x,inf))


$$\lim_{x\rightarrow \infty }{\frac{\sqrt{x^2-3\,x}}{x+1}}=1$$\>$limit((x^3-13\*x^2+51\*x-63)/(x^3-4\*x^2-3\*x+18),x,3)


$$-\frac{4}{5}$$$$\lim_{x\rightarrow 3}{\frac{x^3-13\,x^2+51\,x-63}{x^3-4\,x^2-3\,x+  18}}=-\frac{4}{5}$$Fungsi tersebut diskontinu di titik x=3. Berikut adalah grafik
fungsinya.


\>aspect(1.5); plot2d("(x^3-13\*x^2+51\*x-63)/(x^3-4\*x^2-3\*x+18)",0,4); plot2d(3,-4/5,\>points,style="ow",\>add):


![images/EMT4Kalkulus%20(1)-026.png](images/EMT4Kalkulus%20(1)-026.png)

\>$limit(2\*x\*sin(x)/(1-cos(x)),x,0)


$$4$$$$2\,\left(\lim_{x\rightarrow 0}{\frac{x\,\sin x}{1-\cos x}}\right)=4$$Fungsi tersebut diskontinu di titik x=0. Berikut adalah grafik
fungsinya.


\>plot2d("2\*x\*sin(x)/(1-cos(x))",-pi,pi); plot2d(0,4,\>points,style="ow",\>add):


![images/EMT4Kalkulus%20(1)-029.png](images/EMT4Kalkulus%20(1)-029.png)

\>$limit(cot(7\*h)/cot(5\*h),h,0)


$$\frac{5}{7}$$$$\lim_{h\rightarrow 0}{\frac{\cot \left(7\,h\right)}{\cot \left(5\,h  \right)}}=\frac{5}{7}$$Fungsi tersebut juga diskontinu (karena tidak terdefinisi) di x=0.
Berikut adalah grafiknya.


\>plot2d("cot(7\*x)/cot(5\*x)",-0.001,0.001); plot2d(0,5/7,\>points,style="ow",\>add):


![images/EMT4Kalkulus%20(1)-032.png](images/EMT4Kalkulus%20(1)-032.png)

\>$showev('limit(((x/8)^(1/3)-1)/(x-8),x,8))


$$\lim_{x\rightarrow 8}{\frac{\frac{x^{\frac{1}{3}}}{2}-1}{x-8}}=
 \frac{1}{24}$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("((x/8)^(1/3)-1)/(x-8)", 7.9, 8.1):


![images/EMT4Kalkulus%20(1)-034.png](images/EMT4Kalkulus%20(1)-034.png)

\>$showev('limit(1/(2\*x-1),x,0))


$$\lim_{x\rightarrow 0}{\frac{1}{2\,x-1}}=-1$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("1/(2\*x-1)", -1, 1):


![images/EMT4Kalkulus%20(1)-036.png](images/EMT4Kalkulus%20(1)-036.png)

\>$showev('limit((x^2-3\*x-10)/(x-5),x,5))


$$\lim_{x\rightarrow 5}{\frac{x^2-3\,x-10}{x-5}}=7$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("((x^2 - 3\*x - 10)/(x - 5))", 4, 6) :


![images/EMT4Kalkulus%20(1)-038.png](images/EMT4Kalkulus%20(1)-038.png)

\>$showev('limit(sqrt(x^2+x)-x,x,inf))


$$\lim_{x\rightarrow \infty }{\sqrt{x^2+x}-x}=\frac{1}{2}$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("sqrt(x^2 + x) - x", 1, 100):


![images/EMT4Kalkulus%20(1)-040.png](images/EMT4Kalkulus%20(1)-040.png)

\>$showev('limit(abs(x-1)/(x-1),x,1,minus))


$$\lim_{x\uparrow 1}{\frac{\left| x-1\right| }{x-1}}=-1$$Hitung limit di atas untuk x menuju 1 dari kanan.


Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>$showev('limit(sin(x)/x,x,0))


$$\lim_{x\rightarrow 0}{\frac{\sin x}{x}}=1$$\>plot2d("sin(x)/x",-pi,pi); plot2d(0,1,\>points,style="ow",\>add):


![images/EMT4Kalkulus%20(1)-043.png](images/EMT4Kalkulus%20(1)-043.png)

\>$showev('limit(sin(x^3)/x,x,0))


$$\lim_{x\rightarrow 0}{\frac{\sin x^3}{x}}=0$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("sin(x^3)/x", -0.1, 0.1):


![images/EMT4Kalkulus%20(1)-045.png](images/EMT4Kalkulus%20(1)-045.png)

\>$showev('limit(log(x), x, minf))


$$\lim_{x\rightarrow  -\infty }{\log x}={\it infinity}$$\>$showev('limit((-2)^x,x, inf))


$$\lim_{x\rightarrow \infty }{\left(-2\right)^{x}}={\it infinity}$$\>$showev('limit(t-sqrt(2-t),t,2,minus))


$$\lim_{t\uparrow 2}{t-\sqrt{2-t}}=2$$\>$showev('limit(t-sqrt(2-t),t,2,plus))


$$\lim_{t\downarrow 2}{t-\sqrt{2-t}}=2$$\>$showev('limit(t-sqrt(2-t),t,5,plus)) // Perhatikan hasilnya


$$\lim_{t\downarrow 5}{t-\sqrt{2-t}}=5-\sqrt{3}\,i$$\>plot2d("x-sqrt(2-x)",0,2):


![images/EMT4Kalkulus%20(1)-051.png](images/EMT4Kalkulus%20(1)-051.png)

\>$showev('limit((x^2-9)/(2\*x^2-5\*x-3),x,3))


$$\lim_{x\rightarrow 3}{\frac{x^2-9}{2\,x^2-5\,x-3}}=\frac{6}{7}$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("((x^2 - 9)/(2\*x^2 - 5\*x - 3))", 2, 4):


![images/EMT4Kalkulus%20(1)-053.png](images/EMT4Kalkulus%20(1)-053.png)

\>$showev('limit((1-cos(x))/x,x,0))


$$\lim_{x\rightarrow 0}{\frac{1-\cos x}{x}}=0$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("((1-cos(x))/x)", -0.1, 0.1):


![images/EMT4Kalkulus%20(1)-055.png](images/EMT4Kalkulus%20(1)-055.png)

\>$showev('limit((x^2+abs(x))/(x^2-abs(x)),x,0))


$$\lim_{x\rightarrow 0}{\frac{\left| x\right| +x^2}{x^2-\left| x
 \right| }}=-1$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("((x^2+abs(x))/(x^2-abs(x)))", -0.1, 0.1):


![images/EMT4Kalkulus%20(1)-057.png](images/EMT4Kalkulus%20(1)-057.png)

\>$showev('limit((1+1/x)^x,x,inf))


$$\lim_{x\rightarrow \infty }{\left(\frac{1}{x}+1\right)^{x}}=e$$\>plot2d("(1+1/x)^x",0,1000):


![images/EMT4Kalkulus%20(1)-059.png](images/EMT4Kalkulus%20(1)-059.png)

\>$showev('limit((1+k/x)^x,x,inf))


$$\lim_{x\rightarrow \infty }{\left(\frac{k}{x}+1\right)^{x}}=e^{k}$$\>$showev('limit((1+x)^(1/x),x,0))


$$\lim_{x\rightarrow 0}{\left(x+1\right)^{\frac{1}{x}}}=e$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("((1+x)^(1/x))", -0.1, 0.1):


![images/EMT4Kalkulus%20(1)-062.png](images/EMT4Kalkulus%20(1)-062.png)

\>$showev('limit((x/(x+k))^x,x,inf))


$$\lim_{x\rightarrow \infty }{\left(\frac{x}{x+k}\right)^{x}}=e^ {- k
  }$$\>$showev('limit((E^x-E^2)/(x-2),x,2))


$$\lim_{x\rightarrow 2}{\frac{e^{x}-e^2}{x-2}}=e^2$$Tunjukkan limit tersebut dengan grafik, seperti contoh-contoh sebelumnya.


\>plot2d("((exp(x)-exp(2))/(x-2))", 1.5, 2.5):


![images/EMT4Kalkulus%20(1)-065.png](images/EMT4Kalkulus%20(1)-065.png)

\>$showev('limit(sin(1/x),x,0))


$$\lim_{x\rightarrow 0}{\sin \left(\frac{1}{x}\right)}={\it ind}$$\>$showev('limit(sin(1/x),x,inf))


$$\lim_{x\rightarrow \infty }{\sin \left(\frac{1}{x}\right)}=0$$\>plot2d("sin(1/x)",-0.001,0.001):


![images/EMT4Kalkulus%20(1)-068.png](images/EMT4Kalkulus%20(1)-068.png)

# Latihan

Bukalah buku Kalkulus. Cari dan pilih beberapa (paling sedikit 5 fungsi berbeda
tipe/bentuk/jenis) fungsi dari buku tersebut, kemudian definisikan di EMT pada
baris-baris perintah berikut (jika perlu tambahkan lagi). Untuk setiap fungsi, hitung
nilai limit fungsi tersebut di beberapa nilai dan di tak hingga. Gambar grafik fungsi
tersebut untuk mengkonfirmasi nilai-nilai limit tersebut.


\>$showev('limit(sqrt(x+16),x,inf))


$$\lim_{x\rightarrow \infty }{\sqrt{x+16}}=\infty $$\>$showev('limit(sqrt(x+16),x,0))


$$\lim_{x\rightarrow 0}{\sqrt{x+16}}=4$$\>$showev('limit(sqrt(x+16),x,4))


$$\lim_{x\rightarrow 4}{\sqrt{x+16}}=2\,\sqrt{5}$$\>plot2d("sqrt(x+16)",-7,7); plot2d(0,4,\>points,style="ow",\>add):


![images/EMT4Kalkulus%20(1)-072.png](images/EMT4Kalkulus%20(1)-072.png)

\> 

\>$showev('limit(((x^2)+(2\*x)),x,0,plus))


$$\lim_{x\downarrow 0}{x^2+2\,x}=0$$\>$showev('limit(((x^2)+(2\*x)),x,2,minus))


$$\lim_{x\uparrow 2}{x^2+2\,x}=8$$\>$showev('limit(((x^2)+(2\*x)),x,inf))


$$\lim_{x\rightarrow \infty }{x^2+2\,x}=\infty $$\>plot2d("((x^2)+(2\*x))",0,8):


![images/EMT4Kalkulus%20(1)-076.png](images/EMT4Kalkulus%20(1)-076.png)

\> 

\>$showev('limit((1-cos(x))/x^2,x,0))


$$\lim_{x\rightarrow 0}{\frac{1-\cos x}{x^2}}=\frac{1}{2}$$\>$showev('limit((1-cos(x))/x^2,x,inf))


$$\lim_{x\rightarrow \infty }{\frac{1-\cos x}{x^2}}=0$$\>$showev('limit((1-cos(x))/x^2,x,2))


$$\lim_{x\rightarrow 2}{\frac{1-\cos x}{x^2}}=\frac{1}{4}-\frac{\cos 
 2}{4}$$\>plot2d("(1-cos(x))/x^2",-3,3):


![images/EMT4Kalkulus%20(1)-080.png](images/EMT4Kalkulus%20(1)-080.png)

\> 

\>$showev('limit((x^2+2\*x+6),x,3))


$$\lim_{x\rightarrow 3}{x^2+2\,x+6}=21$$\>$showev('limit((x^2+2\*x+6),x,2))


$$\lim_{x\rightarrow 2}{x^2+2\,x+6}=14$$\>$showev('limit((x^2+2\*x+6),x,inf))


$$\lim_{x\rightarrow \infty }{x^2+2\,x+6}=\infty $$\>plot2d("(x^2+2\*x+6)",-6,6); plot2d(3,21,\>points,style="ow",\>add):


![images/EMT4Kalkulus%20(1)-084.png](images/EMT4Kalkulus%20(1)-084.png)

\>$showev('limit((x^4 + 2\*x^3 - x^2)/(x^2),x,0))


$$\lim_{x\rightarrow 0}{\frac{x^4+2\,x^3-x^2}{x^2}}=-1$$\>$showev('limit((x^4 + 2\*x^3 - x^2)/(x^2),x,2))


$$\lim_{x\rightarrow 2}{\frac{x^4+2\,x^3-x^2}{x^2}}=7$$\>$showev('limit((x^4 + 2\*x^3 - x^2)/(x^2),x,inf))


$$\lim_{x\rightarrow \infty }{\frac{x^4+2\,x^3-x^2}{x^2}}=\infty $$\>plot2d("(x^4 + 2\*x^3 - x^2)",-2,2); plot2d(0,-1,\>points,style="ow",\>add):


![images/EMT4Kalkulus%20(1)-088.png](images/EMT4Kalkulus%20(1)-088.png)

# Turunan Fungsi

Definisi turunan:


$$f'(x) = \lim_{h\to 0} \frac{f(x+h)-f(x)}{h}$$Berikut adalah contoh-contoh menentukan turunan fungsi dengan
menggunakan definisi turunan (limit).


\>$showev('limit(((x+h)^2-x^2)/h,h,0)) // turunan x^2


$$\lim_{h\rightarrow 0}{\frac{\left(x+h\right)^2-x^2}{h}}=2\,x$$\>p &= expand((x+h)^2-x^2)|simplify; $p //pembilang dijabarkan dan disederhanakan


$$2\,h\,x+h^2$$\>q &=ratsimp(p/h); $q // ekspresi yang akan dihitung limitnya disederhanakan


$$2\,x+h$$\>$limit(q,h,0) // nilai limit sebagai turunan


$$2\,x$$\>$showev('limit(((x+h)^n-x^n)/h,h,0)) // turunan x^n


$$\lim_{h\rightarrow 0}{\frac{\left(x+h\right)^{n}-x^{n}}{h}}=n\,x^{n
 -1}$$Mengapa hasilnya seperti itu? Tuliskan atau tunjukkan bahwa hasil
limit tersebut benar, sehingga benar turunan fungsinya benar.  Tulis
penjelasan Anda di komentar ini.


Sebagai petunjuk, ekspansikan (x+h)^n dengan menggunakan teorema
binomial.


Petunjuk: ekspansikan (x+h)^n dengan menggunakan teorema binomial.


$$\text{Akan ditunjukkan bahwa \: $f'(x)=\lim_{h\to 0} \frac{(x+h)^n-x^n}{h}=nx^{n-1}$}$$$$\text{Pertama, ekspansikan $(x+h)^n$, yakni: }$$$$\text{$(x+h)^n=\sum_{k=0}^{n} \binom{n}{k}x^{n-k}h^k$}$$$$\text{$\Leftrightarrow \: (x+h)^n=\binom{n}{0}x^{n}+\binom{n}{1}x^{n-1}h+\binom{n}{2}x^{n-2}h^2+ ...+\binom{n}{n}h^n$}$$$$\text{$\Leftrightarrow \: (x+h)^n=x^{n}+nx^{n-1}h+\binom{n}{2}x^{n-2}h^2+\binom{n}{3}x^{n-3}h^3+ ...+h^n$}$$$$\text{Sehingga, $f'(x)$ menjadi:\: $f'(x)=\lim_{h\to 0} \frac{(x+h)^n-x^n}{h}$}$$$$\text{$\Leftrightarrow f'(x)=\lim_{h\to 0} \frac{x^{n}+nx^{n-1}h+\binom{n}{2}x^{n-2}h^2+\binom{n}{3}x^{n-3}h^3+ ...+h^n-x^n}{h}$}$$$$\text{$\Leftrightarrow f'(x)=\lim_{h\to 0} nx^{n-1}+\binom{n}{2}x^{n-2}h+\binom{n}{3}x^{n-3}h^2+ ...+h^{n-1}$}$$$$\text{$\Leftrightarrow f'(x)=nx^{n-1}$. Terbukti.}$$\>$showev('limit((sin(x+h)-sin(x))/h,h,0)) // turunan sin(x)


$$\lim_{h\rightarrow 0}{\frac{\sin \left(x+h\right)-\sin x}{h}}=\cos 
 x$$Mengapa hasilnya seperti itu? Tuliskan atau tunjukkan bahwa hasil
limit tersebut


benar, sehingga benar turunan fungsinya benar.  Tulis penjelasan Anda
di komentar ini.


Sebagai petunjuk, ekspansikan sin(x+h) dengan menggunakan rumus jumlah
dua sudut.


Petunjuk: ekspansikan sin(x+h) dengan menggunakan rumus jumlah dua
sudut.


$$\text{Akan ditunjukkan bahwa \: $\lim_{h\to 0} \frac{sin(x+h)-sin (x)}{h}=cos (x)$}$$$$\text{Pertama, gunakan rumus jumlah sudut untuk $sin(x+h)$, yakni: }$$$$sin(x+h)=sin(x)cos(h)+cos(x)sin(h)$$$$\iff \lim_{h \to 0} \frac{\sin(x+h) - \sin(x)}{h} = \lim_{h \to 0} \frac{[\sin(x)\cos(h) + \cos(x)\sin(h)] - \sin(x)}{h}$$$$\iff \lim_{h \to 0} \frac{\sin(x)\cos(h) + \cos(x)\sin(h) - \sin(x)}{h}$$$$\iff \lim_{h \to 0} \left( \frac{\sin(x)[\cos(h) - 1]}{h} + \frac{\cos(x)\sin(h)}{h} \right)$$$$\text{Diketahui bahwa:}$$$$\text{$1).\: \lim_{h\to 0} \frac{cos(h)\--1}{h}=0$}$$$$\text{$2).\: \lim_{h\to 0} \frac{\sin (h)}{h}=1$}$$$$\text{sehingga: }$$$$\iff \lim_{h \to 0} \left[ \sin(x)(0) + \cos(x)(1) \right]$$$$\text{$\Leftrightarrow 0 + cos (x) = cos (x)$. Terbukti.}$$\>$showev('limit((log(x+h)-log(x))/h,h,0)) // turunan log(x)


$$\lim_{h\rightarrow 0}{\frac{\log \left(x+h\right)-\log x}{h}}=
 \frac{1}{x}$$Mengapa hasilnya seperti itu? Tuliskan atau tunjukkan bahwa hasil
limit tersebut


benar, sehingga benar turunan fungsinya benar.  Tulis penjelasan Anda
di komentar ini.


Sebagai petunjuk, gunakan sifat-sifat logaritma dan hasil limit pada
bagian sebelumnya di atas.


$$\text{Akan ditunjukkan bahwa\: $\lim_{h\to 0} \frac{\log(x+h)-\log x}{h}=\frac {1}{x}$}$$$$\text{$\lim_{h\to 0} \frac{\log(x+h)-\log (x)}{h}$}$$$$\text{Diketahui bahwa:}$$$$\text{$\log(a)-\log(b)=\log(\frac{a}{b})$}$$$$\text{Sehingga:}$$$$\text{$=\lim_{h\to 0} \frac{\log\left(\frac{x+h}{x}\right)}{h}$}$$$$\text{$=\lim_{h\to 0} \frac{\log\left(1+\frac{h}{x}\right)}{h}$}$$$$\text{Diketahui bahwa:}$$$$\text{$\lim_{h\to 0} \frac{\log(1+u)}{u}=1$}$$$$\text{dengan\: $u=\frac{h}{x}$}$$$$\text{Sehingga:}$$$$\text{$f'(x)= \frac{1}{x}\times x $}$$$$\text{$f'(x)= \frac{1}{x}$}$$$$\text{$\lim_{h\to 0} \frac{\log(x+h)-\log x}{h}=\frac {1}{x}$. Terbukti.}$$\>$showev('limit((1/(x+h)-1/x)/h,h,0)) // turunan 1/x


$$\lim_{h\rightarrow 0}{\frac{\frac{1}{x+h}-\frac{1}{x}}{h}}=-\frac{1
 }{x^2}$$\>$showev('limit((E^(x+h)-E^x)/h,h,0)) // turunan f(x)=e^x


    Answering "Is x an integer?" with "integer"
    Answering "Is x an integer?" with "integer"
    Answering "Is x an integer?" with "integer"
    Answering "Is x an integer?" with "integer"
    Answering "Is x an integer?" with "integer"
    Maxima is asking
    Acceptable answers are: yes, y, Y, no, n, N, unknown, uk
    Is x an integer?
    
    Use assume!
    Error in:
    $showev('limit((E^(x+h)-E^x)/h,h,0)) // turunan f(x)=e^x ...
                                         ^

Maxima bermasalah dengan limit:


$$\lim_{h\to 0}\frac{e^{x+h}-e^x}{h}.$$Oleh karena itu diperlukan trik khusus agar hasilnya benar.


\>$showev('limit((E^h-1)/h,h,0))


$$\lim_{h\rightarrow 0}{\frac{e^{h}-1}{h}}=1$$\>$showev('factor(E^(x+h)-E^x))


$${\it factor}\left(e^{x+h}-e^{x}\right)=\left(e^{h}-1\right)\,e^{x}$$\>$showev('limit(factor((E^(x+h)-E^x)/h),h,0)) // turunan f(x)=e^x


$$\left(\lim_{h\rightarrow 0}{\frac{e^{h}-1}{h}}\right)\,e^{x}=e^{x}$$\>function f(x) &= x^x


    
                                       x
                                      x
    

\>$showev('limit(f(x),x,0))


$$\lim_{x\rightarrow 0}{x^{x}}=1$$Silakan Anda gambar kurva


$$y=x^x.$$\>plot2d("x^x"):


![images/EMT4Kalkulus%20(1)-139.png](images/EMT4Kalkulus%20(1)-139.png)

\>$showev('limit((f(x+h)-f(x))/h,h,0)) // turunan f(x)=x^x


$$\lim_{h\rightarrow 0}{\frac{\left(x+h\right)^{x+h}-x^{x}}{h}}=
 {\it infinity}$$Di sini Maxima juga bermasalah terkait limit:


$$\lim_{h\to 0} \frac{(x+h)^{x+h}-x^x}{h}.$$Dalam hal ini diperlukan asumsi nilai x.


Dapat dilihat bahwa dari yang kita cari pertama nilai limit dari


$$x^x$$itu ada yaitu 1.


Sementara pada yang kita cari menggunakan definisi turunan nilai
limitnya infinity.


Begitu juga pada grafik, nilai dari x hanya terdefinisi di zona
positif, jadi untuk mencari turunannya perlu diasumsikan dulu bahwa
nilai x nya itu berjalan dengan x yang positif karena nilai dari yang
negatifnya tidak terdefinisi.


\>&assume(x\>0); $showev('limit((f(x+h)-f(x))/h,h,0)) // turunan f(x)=x^x


$$\lim_{h\rightarrow 0}{\frac{\left(x+h\right)^{x+h}-x^{x}}{h}}=x^{x}
 \,\left(\log x+1\right)$$Mengapa hasilnya seperti itu? Tuliskan atau tunjukkan bahwa hasil
limit tersebut benar, sehingga benar turunan fungsinya benar. Tulis
penjelasan Anda di komentar ini.


$$\text{Akan ditunjukkan bahwa\: $\lim_{h\to 0} \frac{(x+h)^{x+h}-x^x}{h}=x^x(\log(x)+1)$}$$$$\text{Menggunakan logaritma untuk menyederhanakan}$$$$y=x^x$$$$log(y)=log(x^x)=x log(x)$$$$\frac{1}{y}\frac{d}{dx}=\frac{d}{dx}(x log(x))$$$$\frac{1}{y}\frac{d}{dx}=\log(x)+1$$$$\text{Substitusi kembali}$$$$y=x^x, sehingga$$$$\frac{d}{dx}=x^x(log(x)+1)$$\>&forget(x\>0) // jangan lupa, lupakan asumsi untuk kembali ke semula


    
                                   [x &gt; 0]
    

\>&forget(x<0)


    
                                   [x &lt; 0]
    

\>&facts()


    
                                      []
    

\>$showev('limit((asin(x+h)-asin(x))/h,h,0)) // turunan arcsin(x)


$$\lim_{h\rightarrow 0}{\frac{\arcsin \left(x+h\right)-\arcsin x}{h}}=
 \frac{1}{\sqrt{1-x^2}}$$Mengapa hasilnya seperti itu? Tuliskan atau tunjukkan bahwa hasil
limit tersebut benar, sehingga benar turunan fungsinya benar. Tulis
penjelasan Anda di komentar ini.


$$f'(x) = \lim_{h\to 0} \frac{arcsin(x+h)-arcsinx}{h}$$$$arcsin(x+h)=A, arcsinx=B$$$$sinA=x+h, sinB=x$$$$sinA-sinB=(x+h)-x$$$$\frac{d}{dx}(arcsin x) =\displaystyle \lim_{A \to B} \frac{A- B}{Sin A- Sin B}$$$$\frac{d}{dx}(arcsin x) =\displaystyle \lim_{A \to B} \frac{A- B}{2Cos \frac{A+B}{2}- 2 Sin \frac{A-B}{2}}$$$$\frac{d}{dx}(arcsin x) =\displaystyle \lim_{A \to B} \frac{\frac{A- B}{2}}{Sin \frac{A-B}{2}}\times \frac{1}{Cos \frac{A+B}{2}}$$$$\frac{d}{dx}(arcsin x) ={1}\times \frac{1}{Cos \frac{B+B}{2}}$$$$\frac{d}{dx}(arcsin x) =\frac{1}{Cos {B}}$$$$sin2 y+cos2 y = 1$$$$cos B =\frac{1}{\sqrt{1-sin^2B}}=\frac{1}{\sqrt{1-x^2}}$$$$f'(x)=\frac{dy}{dx} =\frac{1}{\sqrt{1-x^2}}$$\>$showev('limit((tan(x+h)-tan(x))/h,h,0)) // turunan tan(x)


$$\lim_{h\rightarrow 0}{\frac{\tan \left(x+h\right)-\tan x}{h}}=
 \frac{1}{\cos ^2x}$$Mengapa hasilnya seperti itu? Tuliskan atau tunjukkan bahwa hasil
limit tersebut benar, sehingga benar turunan fungsinya benar. Tulis
penjelasan Anda di komentar ini.


$$f'(x) = \lim_{h\to 0} \frac{tan(x+h)-tan(x)}{h}$$$$tan(x+h)=\frac{tan(x)+tan(h}{1-tan(x)tan(h)}$$$$tan(x+h)-tan(x)=\frac{tan(x)+tan(h}{1-tan(x)tan(h)}-tan(x)$$$$\frac{tan(x)+tan(h)-tan(x)(1-tan(x)tan(h))}{1-tan(x)tan(h)}=\frac{tan(h)+tan^2(x)tan(h)}{1-tan(x)tan(h)}$$$$=\frac{tan(h)(1+tan^2(x))}{1-tan(x)tan(h)}$$$$= \lim_{h\to 0}\frac{h(1+tan^2(x))}{1-tan(x)h}$$$$=\lim_{h\to 0}\frac{h(1+tan^2(x))}{1}$$$$=\lim_{h\to 0}h(1+tan^2(x))$$$$=\lim_{h\to 0}\frac{h(1+tan^2(x))}{h}$$$$=1+tan^2(x)$$$$=1+tan^2(x)=sec^2(x)$$$$f'(x)=sec^2(x)=\frac{1}{cos^2(x)}$$Jadi, terbukti benar bahwa


$$= f'(x) = \lim_{h\to 0} \frac{tan(x+h)-tan(x)}{h}=\frac{1}{cos^2(x)}$$\>function f(x) &= sinh(x) // definisikan f(x)=sinh(x)


    
                                   sinh(x)
    

\>function df(x) &= limit((f(x+h)-f(x))/h,h,0); $df(x) // df(x) = f'(x)


$$\frac{e^ {- x }\,\left(e^{2\,x}+1\right)}{2}$$Hasilnya adalah cosh(x), karena


$$\frac{e^x+e^{-x}}{2}=\cosh(x).$$\>plot2d(["f(x)","df(x)"],-pi,pi,color=[blue,red]):


![images/EMT4Kalkulus%20(1)-182.png](images/EMT4Kalkulus%20(1)-182.png)

\>function f(x) &= sin(3\*x^5+7)^2


    
                                   2    5
                                sin (3 x  + 7)
    

\>diff(f,3), diffc(f,3)


    1198.32948904
    1198.72863721

Apakah perbedaan diff dan diffc?


diff untuk menghitung turunan numerik ke-n dari fungsi f menggunakan
metode perbedaan terbatas (finite difference). Sedangkan diffc mungkin
merujuk pada metode yang lebih canggih atau terkompensasi untuk
menghitung turunan numerik ke-n dari fungsi f.


\>$showev('diff(f(x),x))


$$\frac{d}{d\,x}\,\sin ^2\left(3\,x^5+7\right)=30\,x^4\,\cos \left(3
 \,x^5+7\right)\,\sin \left(3\,x^5+7\right)$$\>$% with x=3


$${\it \%at}\left(\frac{d}{d\,x}\,\sin ^2\left(3\,x^5+7\right) , x=3
 \right)=2430\,\cos 736\,\sin 736$$\>$float(%)


$${\it \%at}\left(\frac{d^{1.0}}{d\,x^{1.0}}\,\sin ^2\left(3.0\,x^5+
 7.0\right) , x=3.0\right)=1198.728637211748$$\>plot2d(f,0,3.1):


![images/EMT4Kalkulus%20(1)-186.png](images/EMT4Kalkulus%20(1)-186.png)

\>function f(x) &=5\*cos(2\*x)-2\*x\*sin(2\*x) // mendifinisikan fungsi f


    
                          5 cos(2 x) - 2 x sin(2 x)
    

\>function df(x) &=diff(f(x),x) // fd(x) = f'(x)


    
                         - 12 sin(2 x) - 4 x cos(2 x)
    

\>$'f(1)=f(1), $float(f(1)), $'f(2)=f(2), $float(f(2)) // nilai f(1) dan f(2)


$$f\left(1\right)=5\,\cos 2-2\,\sin 2$$$$-3.899329036387075$$$$f\left(2\right)=5\,\cos 4-4\,\sin 4$$$$-0.2410081230863468$$\>xp=solve("df(x)",1,2,0) // solusi f'(x)=0 pada interval [1, 2]


    1.35822987384

\>df(xp), f(xp) // cek bahwa f'(xp)=0 dan nilai ekstrim di titik tersebut


    0
    -5.67530133759

\>plot2d(["f(x)","df(x)"],0,2\*pi,color=[blue,red]): //grafik fungsi dan turunannya


![images/EMT4Kalkulus%20(1)-191.png](images/EMT4Kalkulus%20(1)-191.png)

Perhatikan titik-titik "puncak" grafik y=f(x) dan nilai turunan pada saat grafik fungsinya mencapai titik "puncak" tersebut.


# Latihan

Bukalah buku Kalkulus. Cari dan pilih beberapa (paling sedikit 5
fungsi berbeda tipe/bentuk/jenis) fungsi dari buku tersebut, kemudian
definisikan di EMT pada baris-baris perintah berikut (jika perlu
tambahkan lagi). Untuk setiap fungsi, tentukan turunannya dengan
menggunakan definisi turunan (limit), menggunakan perintah diff, dan
secara manual (langkah demi langkah yang dihitung dengan Maxima)
seperti contoh-contoh di atas. Gambar grafik fungsi asli dan fungsi
turunannya pada sumbu koordinat yang sama.


                                1  

\>function f(x) &= E^(3\*x)+4\*x\*E^x


    
                 4.999975000072321e-7 r
            [1, E
                               1.66665833335744e-7 r
     + 6.666633333429761e-7 r E                     , 
     3.999920000760659e-6 r
    E                       + 5.333226667680879e-6 r
      1.33330666692022e-6 r   1.34993925130153e-5 r
     E                     , E
                               4.499797504338432e-6 r
     + 1.799919001735373e-5 r E                      , 
     3.199744009751981e-5 r
    E                       + 4.266325346335975e-5 r
      1.066581336583994e-5 r   6.249218796501588e-5 r
     E                      , E
                               2.083072932167196e-5 r
     + 8.332291728668784e-5 r E                      , 
     1.079805616662072e-4 r
    E                       + 1.439740822216096e-4 r
      3.599352055540239e-5 r   1.714579874017158e-4 r
     E                      , E
                               5.71526624672386e-5 r
     + 2.286106498689544e-4 r E                     , 
     2.559180924819188e-4 r
    E                       + 3.41224123309225e-4 r
      8.530603082730626e-5 r   3.643524059668696e-4 r
     E                      , E
                               1.214508019889565e-4 r
     + 4.858032079558261e-4 r E                      , 
     4.997500595155524e-4 r
    E                       + 6.663334126874032e-4 r
      1.665833531718508e-4 r   6.650974884755689e-4 r
     E                      , E
                               2.216991628251896e-4 r
     + 8.867966513007586e-4 r E                      , 
     8.633781332419016e-4 r
    E                       + 0.001151170844322535 r
      2.877927110806339e-4 r   0.001097572140915437 r
     E                      , E
                               3.658573803051457e-4 r
     + 0.001463429521220583 r E                      , 
     0.00137065606729056 r
    E                      + 0.00182754142305408 r
      4.568853557635201e-4 r   0.001685602579202333 r
     E                      , E
                               5.618675264007778e-4 r
     + 0.002247470105603111 r E                      , 
     0.002045380157262078 r
    E                       + 0.002727173543016104 r
      6.817933857540259e-4 r   0.002452952799011948 r
     E                      , E
                               8.176509330039827e-4 r
     + 0.003270603732015931 r E                      , 
     0.002911279722527443 r
    E                       + 0.003881706296703258 r
      9.704265741758145e-4 r   0.003423315070498284 r
     E                      , E
                               0.001141105023499428 r
     + 0.004564420093997712 r E                      , 
     0.003992007614816384 r
    E                       + 0.005322676819755179 r
      0.001330669204938795 r   0.00462030046170131 r
     E                      , E
                               0.001540100153900437 r
     + 0.006160400615601747 r E                      , 
     0.005311130757392035 r
    E                       + 0.007081507676522714 r
      0.001770376919130678 r   0.006067429394434803 r
     E                      , E
                               0.002022476464811601 r
     + 0.008089905859246405 r E                      , 
     0.00689212071859624 r
    E                      + 0.009189494291461653 r
      0.002297373572865413 r   0.007788122236431189 r
     E                      , E
                              0.002596040745477063 r
     + 0.01038416298190825 r E                      , 
     0.008758344323534673 r
    E                       + 0.01167779243137956 r
      0.002919448107844891 r   0.009805689933506612 r
     E                      , E
                              0.003268563311168871 r
     + 0.01307425324467548 r E                      , 
     0.01093305430765878 r
    E                      + 0.01457740574354505 r
      0.003644351435886262 r   0.01214332468549334 r
     E                      , E
                              0.004047774895164447 r
     + 0.01619109958065779 r E                      , 
     0.01343938001598133 r
    E                      + 0.01791917335464177 r
      0.004479793338660443 r   0.0148240906696695 r
     E                      , E
                            0.0049413635565565 r
     + 0.019765454226226 r E                    , 
     0.01630031815164673 r
    E                      + 0.02173375753552897 r
      0.005433439383882244 r   0.01787091481539493 r
     E                      , E
                              0.005956971605131645 r
     + 0.02382788642052658 r E                      , 
     0.01953872357755687 r
    E                      + 0.0260516314367425 r
      0.006512907859185624 r   0.02130657763364591 r
     E                      , E
                              0.007102192544548636 r
     + 0.02840877017819454 r E                      , 
     0.02317730017473013 r
    E                      + 0.03090306689964017 r
      0.007725766724910044 r   0.02515370410511403 r
     E                      , E
                              0.00838456803503801 r
     + 0.03353827214015204 r E                     , 
     0.02723859176105198 r
    E                      + 0.0363181223480693 r
      0.009079530587017326 r   0.02943475463051576 r
     E                      , E
                              0.009811584876838586 r
     + 0.03924633950735434 r E                      , 
     0.0317449730740485 r                        0.0105816576913495 r
    E                     + 0.042326630765398 r E                    , 
     0.03417201604673142 r
    E                      + 0.04556268806230857 r
      0.01139067201557714 r   0.03671864082128951 r
     E                     , E
                              0.01223954694042984 r
     + 0.04895818776171934 r E                     , 
     0.03938759271236769 r
    E                      + 0.05251679028315692 r
      0.01312919757078923 r   0.04218160480200134 r
     E                     , E
                              0.01406053493400045 r
     + 0.05624213973600178 r E                     , 
     0.0451033976663095 r                          0.01503446588876983 r
    E                     + 0.06013786355507933 r E                     , 
     0.04815567910344071 r
    E                      + 0.06420757213792094 r
      0.01605189303448024 r   0.05134114386279526 r
     E                     , E
                              0.01711371462093175 r
     + 0.06845485848372701 r E                     , 
     0.05466247337555141 r
    E                      + 0.07288329783406855 r
      0.01822082445851714 r   0.05812233548652607 r
     E                     , E
                              0.01937411182884202 r
     + 0.07749644731536809 r E                     , 
     0.06172338418739115 r                         0.02057446139579705 r
    E                      + 0.0822978455831882 r E                     , 
     0.06546825935127759 r
    E                      + 0.08729101246837012 r
      0.02182275311709253 r   0.06935958646878998 r
     E                     , E
                             0.02311986215626333 r
     + 0.0924794486250533 r E                     , 
     0.07339997638545925 r
    E                      + 0.09786663518061234 r
      0.02446665879515308 r   0.07759202504066087 r
     E                     , E
                             0.02586400834688696 r
     + 0.1034560333875478 r E                     , 
     0.08193831320802247 r                         0.02731277106934082 r
    E                      + 0.1092510842773633 r E                     , 
     0.08644140623734997 r                         0.02881380207911666 r
    E                      + 0.1152552083164666 r E                     , 
     0.09110385379809227 r                        0.03036795126603076 r
    E                      + 0.121471805064123 r E                     , 
     0.09592818962437955 r                         0.03197606320812652 r
    E                      + 0.1279042528325061 r E                     , 
     0.1009169312616489 r                         0.0336389770872163 r
    E                     + 0.1345559083488652 r E                    , 
     0.1060725798148942 r                         0.03535752660496472 r
    E                     + 0.1414301064198589 r E                     , 
     0.1113976196985564 r                         0.03713253989951881 r
    E                     + 0.1485301595980753 r E                     , 
     0.1168945183880851 r                         0.03896483946269502 r
    E                     + 0.1558593578507801 r E                     , 
     0.1225657261731915 r                        0.0408552420577305 r
    E                     + 0.163420968230922 r E                    , 
     0.128413675912824 r                         0.04280455863760801 r
    E                    + 0.1712182345504321 r E                     , 
     0.1344407827918814 r                         0.04481359426396048 r
    E                     + 0.1792543770558419 r E                     , 
     0.1406494440796987 r                         0.04688314802656623 r
    E                     + 0.1875325921062649 r E                     , 
     0.1470420388903213 r                         0.04901401296344043 r
    E                     + 0.1960560518537617 r E                     , 
     0.1536209279445947 r                         0.05120697598153157 r
    E                     + 0.2048279039261263 r E                     , 
     0.1603884533340966 r                         0.05346281777803219 r
    E                     + 0.2138512711121288 r E                     , 
     0.1673469382869271 r                         0.05578231276230905 r
    E                     + 0.2231292510492362 r E                     , 
     0.1744986869353904 r                         0.05816622897846346 r
    E                     + 0.2326649159138539 r E                     , 
     0.1818459840855809 r                         0.06061532802852698 r
    E                     + 0.2424613121141079 r E                     , 
     0.1893910949889066 r                         0.0631303649963022 r
    E                     + 0.2525214599852088 r E                    , 
     0.1971362651155651 r                         0.06571208837185505 r
    E                     + 0.2628483534874202 r E                     , 
     0.205083719929998 r                        0.06836123997666599 r
    E                    + 0.273444959906664 r E                     , 
     0.2132356646683464 r                         0.07107855488944881 r
    E                     + 0.2843142195577952 r E                     , 
     0.2215942841179303 r                         0.07386476137264342 r
    E                     + 0.2954590454905737 r E                     , 
     0.23016174239877 r                       0.07672058079958999 r
    E                   + 0.30688232319836 r E                     , 
     0.238940182747177 r                         0.07964672758239233 r
    E                    + 0.3185869103295693 r E                     , 
     0.2479317273014321 r                         0.08264390910047736 r
    E                     + 0.3305756364019095 r E                     , 
     0.2571384768895728 r                         0.0857128256298576 r
    E                     + 0.3428513025194304 r E                    , 
     0.2665625108193128 r                         0.08885417027310427 r
    E                     + 0.3554166810924171 r E                     , 
     0.2762058866701123 r                         0.09206862889003742 r
    E                     + 0.3682745155601497 r E                     , 
     0.2860706400874227 r                         0.09535688002914089 r
    E                     + 0.3814275201165636 r E                     , 
     0.2961587845791225 r                       0.0987195948597075 r
    E                     + 0.39487837943883 r E                    , 
     0.3064723113141697 r                        0.1021574371047232 r
    E                     + 0.408629748418893 r E                    , 
     0.3170131889234854 r                         0.1056710629744951 r
    E                     + 0.4226842518979805 r E                    , 
     0.3277833633030928 r                         0.1092611211010309 r
    E                     + 0.4370444844041237 r E                    , 
     0.3387847574195292 r                         0.1129282524731764 r
    E                     + 0.4517130098927056 r E                    , 
     0.3500192711175505 r                         0.1166730903725168 r
    E                     + 0.4666923614900673 r E                    , 
     0.3614887809301494 r                         0.1204962603100498 r
    E                     + 0.4819850412401991 r E                    , 
     0.3731951398909027 r                         0.1243983799636342 r
    E                     + 0.4975935198545369 r E                    , 
     0.3851401773486692 r                         0.1283800591162231 r
    E                     + 0.5135202364648923 r E                    , 
     0.3973256987846578 r                         0.1324418995948859 r
    E                     + 0.5297675983795438 r E                    , 
     0.4097534856318796 r                         0.1365844952106265 r
    E                     + 0.5463379808425062 r E                    , 
     0.4224252950970061 r                         0.140808431699002 r
    E                     + 0.5632337267960081 r E                   , 
     0.4353428599846507 r                        0.1451142866615502 r
    E                     + 0.580457146646201 r E                    , 
     0.4485078885240895 r                         0.1495026295080298 r
    E                     + 0.5980105180321194 r E                    , 
     0.4619220641984394 r                         0.1539740213994798 r
    E                     + 0.6158960855979192 r E                    ]
    

\>$showev('limit(factor((E^(3\*x+h)+4\*(x+h)\*E^(x+h)-E^(3\*x)-4\*x\*E^x)/h),h,0))


    Answering "Is 24036*r/5341573699 an integer?" with "integer"
    Answering "Is 24036*r/5341573699 an integer?" with "integer"
    Answering "Is 24036*r/5341573699 an integer?" with "integer"
    Answering "Is 24036*r/5341573699 an integer?" with "integer"
    Answering "Is 24036*r/5341573699 an integer?" with "integer"
    Maxima is asking
    Acceptable answers are: yes, y, Y, no, n, N, unknown, uk
    Is 24036*r/5341573699 an integer?
    
    Use assume!
    Error in:
    ... (3*x+h)+4*(x+h)*E^(x+h)-E^(3*x)-4*x*E^x)/h),h,0)) ...
                                                         ^

\>function df(x) &= E^x\*(E^(2\*x)+4\*x+4)


    
                 1.66665833335744e-7 r   3.333316666714881e-7 r
            [5, E                      (E
                                     1.33330666692022e-6 r
     + 6.666633333429761e-7 r + 4), E
       2.66661333384044e-6 r
     (E                      + 5.333226667680879e-6 r + 4), 
     4.499797504338432e-6 r   8.999595008676864e-6 r
    E                       (E
                                     1.066581336583994e-5 r
     + 1.799919001735373e-5 r + 4), E
       2.133162673167988e-5 r
     (E                       + 4.266325346335975e-5 r + 4), 
     2.083072932167196e-5 r   4.166145864334392e-5 r
    E                       (E
                                     3.599352055540239e-5 r
     + 8.332291728668784e-5 r + 4), E
       7.198704111080478e-5 r
     (E                       + 1.439740822216096e-4 r + 4), 
     5.71526624672386e-5 r   1.143053249344772e-4 r
    E                      (E
                                     8.530603082730626e-5 r
     + 2.286106498689544e-4 r + 4), E
       1.706120616546125e-4 r
     (E                       + 3.41224123309225e-4 r + 4), 
     1.214508019889565e-4 r   2.42901603977913e-4 r
    E                       (E
                                     1.665833531718508e-4 r
     + 4.858032079558261e-4 r + 4), E
       3.331667063437016e-4 r
     (E                       + 6.663334126874032e-4 r + 4), 
     2.216991628251896e-4 r   4.433983256503793e-4 r
    E                       (E
                                     2.877927110806339e-4 r
     + 8.867966513007586e-4 r + 4), E
       5.755854221612677e-4 r
     (E                       + 0.001151170844322535 r + 4), 
     3.658573803051457e-4 r   7.317147606102914e-4 r
    E                       (E
                                     4.568853557635201e-4 r
     + 0.001463429521220583 r + 4), E
       9.137707115270399e-4 r
     (E                       + 0.00182754142305408 r + 4), 
     5.618675264007778e-4 r   0.001123735052801556 r
    E                       (E
                                     6.817933857540259e-4 r
     + 0.002247470105603111 r + 4), E
       0.001363586771508052 r
     (E                       + 0.002727173543016104 r + 4), 
     8.176509330039827e-4 r   0.001635301866007965 r
    E                       (E
                                     9.704265741758145e-4 r
     + 0.003270603732015931 r + 4), E
       0.001940853148351629 r
     (E                       + 0.003881706296703258 r + 4), 
     0.001141105023499428 r   0.002282210046998856 r
    E                       (E
                                     0.001330669204938795 r
     + 0.004564420093997712 r + 4), E
       0.002661338409877589 r
     (E                       + 0.005322676819755179 r + 4), 
     0.001540100153900437 r   0.003080200307800873 r
    E                       (E
                                     0.001770376919130678 r
     + 0.006160400615601747 r + 4), E
       0.003540753838261357 r
     (E                       + 0.007081507676522714 r + 4), 
     0.002022476464811601 r   0.004044952929623202 r
    E                       (E
                                     0.002297373572865413 r
     + 0.008089905859246405 r + 4), E
       0.004594747145730826 r
     (E                       + 0.009189494291461653 r + 4), 
     0.002596040745477063 r   0.005192081490954126 r
    E                       (E
                                    0.002919448107844891 r
     + 0.01038416298190825 r + 4), E
       0.005838896215689782 r
     (E                       + 0.01167779243137956 r + 4), 
     0.003268563311168871 r   0.006537126622337741 r
    E                       (E
                                    0.003644351435886262 r
     + 0.01307425324467548 r + 4), E
       0.007288702871772523 r
     (E                       + 0.01457740574354505 r + 4), 
     0.004047774895164447 r   0.008095549790328893 r
    E                       (E
                                    0.004479793338660443 r
     + 0.01619109958065779 r + 4), E
       0.008959586677320885 r
     (E                       + 0.01791917335464177 r + 4), 
     0.0049413635565565 r   0.009882727113112999 r
    E                     (E                       + 0.019765454226226 r
            0.005433439383882244 r   0.01086687876776449 r
     + 4), E                       (E
                                    0.005956971605131645 r
     + 0.02173375753552897 r + 4), E
       0.01191394321026329 r
     (E                      + 0.02382788642052658 r + 4), 
     0.006512907859185624 r   0.01302581571837125 r
    E                       (E                      + 0.0260516314367425 r
            0.007102192544548636 r   0.01420438508909727 r
     + 4), E                       (E
                                    0.007725766724910044 r
     + 0.02840877017819454 r + 4), E
       0.01545153344982009 r
     (E                      + 0.03090306689964017 r + 4), 
     0.00838456803503801 r   0.01676913607007602 r
    E                      (E                      + 0.03353827214015204 r
            0.009079530587017326 r   0.01815906117403465 r
     + 4), E                       (E
                                   0.009811584876838586 r
     + 0.0363181223480693 r + 4), E
       0.01962316975367717 r
     (E                      + 0.03924633950735434 r + 4), 
     0.0105816576913495 r   0.021163315382699 r
    E                     (E                    + 0.042326630765398 r
            0.01139067201557714 r   0.02278134403115428 r
     + 4), E                      (E
                                    0.01223954694042984 r
     + 0.04556268806230857 r + 4), E
       0.02447909388085967 r
     (E                      + 0.04895818776171934 r + 4), 
     0.01312919757078923 r   0.02625839514157846 r
    E                      (E                      + 0.05251679028315692 r
            0.01406053493400045 r   0.02812106986800089 r
     + 4), E                      (E
                                    0.01503446588876983 r
     + 0.05624213973600178 r + 4), E
       0.03006893177753966 r
     (E                      + 0.06013786355507933 r + 4), 
     0.01605189303448024 r   0.03210378606896047 r
    E                      (E                      + 0.06420757213792094 r
            0.01711371462093175 r   0.03422742924186351 r
     + 4), E                      (E
                                    0.01822082445851714 r
     + 0.06845485848372701 r + 4), E
       0.03644164891703428 r
     (E                      + 0.07288329783406855 r + 4), 
     0.01937411182884202 r   0.03874822365768404 r
    E                      (E                      + 0.07749644731536809 r
            0.02057446139579705 r   0.0411489227915941 r
     + 4), E                      (E
                                   0.02182275311709253 r
     + 0.0822978455831882 r + 4), E
       0.04364550623418506 r
     (E                      + 0.08729101246837012 r + 4), 
     0.02311986215626333 r   0.04623972431252665 r
    E                      (E                      + 0.0924794486250533 r
            0.02446665879515308 r   0.04893331759030617 r
     + 4), E                      (E
                                    0.02586400834688696 r
     + 0.09786663518061234 r + 4), E
       0.05172801669377391 r
     (E                      + 0.1034560333875478 r + 4), 
     0.02731277106934082 r   0.05462554213868165 r
    E                      (E                      + 0.1092510842773633 r
            0.02881380207911666 r   0.05762760415823331 r
     + 4), E                      (E
                                   0.03036795126603076 r
     + 0.1152552083164666 r + 4), E
       0.06073590253206151 r
     (E                      + 0.121471805064123 r + 4), 
     0.03197606320812652 r   0.06395212641625303 r
    E                      (E                      + 0.1279042528325061 r
            0.0336389770872163 r   0.06727795417443261 r
     + 4), E                     (E
                                   0.03535752660496472 r
     + 0.1345559083488652 r + 4), E
       0.07071505320992943 r
     (E                      + 0.1414301064198589 r + 4), 
     0.03713253989951881 r   0.07426507979903763 r
    E                      (E                      + 0.1485301595980753 r
            0.03896483946269502 r   0.07792967892539004 r
     + 4), E                      (E
                                   0.0408552420577305 r
     + 0.1558593578507801 r + 4), E
       0.081710484115461 r
     (E                    + 0.163420968230922 r + 4), 
     0.04280455863760801 r   0.08560911727521603 r
    E                      (E                      + 0.1712182345504321 r
            0.04481359426396048 r   0.08962718852792095 r
     + 4), E                      (E
                                   0.04688314802656623 r
     + 0.1792543770558419 r + 4), E
       0.09376629605313247 r
     (E                      + 0.1875325921062649 r + 4), 
     0.04901401296344043 r   0.09802802592688087 r
    E                      (E                      + 0.1960560518537617 r
            0.05120697598153157 r   0.1024139519630631 r
     + 4), E                      (E
                                   0.05346281777803219 r
     + 0.2048279039261263 r + 4), E
       0.1069256355560644 r
     (E                     + 0.2138512711121288 r + 4), 
     0.05578231276230905 r   0.1115646255246181 r
    E                      (E                     + 0.2231292510492362 r
            0.05816622897846346 r   0.1163324579569269 r
     + 4), E                      (E
                                   0.06061532802852698 r
     + 0.2326649159138539 r + 4), E
       0.121230656057054 r
     (E                    + 0.2424613121141079 r + 4), 
     0.0631303649963022 r   0.1262607299926044 r
    E                     (E                     + 0.2525214599852088 r
            0.06571208837185505 r   0.1314241767437101 r
     + 4), E                      (E
                                   0.06836123997666599 r
     + 0.2628483534874202 r + 4), E
       0.136722479953332 r
     (E                    + 0.273444959906664 r + 4), 
     0.07107855488944881 r   0.1421571097788976 r
    E                      (E                     + 0.2843142195577952 r
            0.07386476137264342 r   0.1477295227452868 r
     + 4), E                      (E
                                   0.07672058079958999 r
     + 0.2954590454905737 r + 4), E
       0.15344116159918 r
     (E                   + 0.30688232319836 r + 4), 
     0.07964672758239233 r   0.1592934551647847 r
    E                      (E                     + 0.3185869103295693 r
            0.08264390910047736 r   0.1652878182009547 r
     + 4), E                      (E
                                   0.0857128256298576 r
     + 0.3305756364019095 r + 4), E
       0.1714256512597152 r
     (E                     + 0.3428513025194304 r + 4), 
     0.08885417027310427 r   0.1777083405462085 r
    E                      (E                     + 0.3554166810924171 r
            0.09206862889003742 r   0.1841372577800748 r
     + 4), E                      (E
                                   0.09535688002914089 r
     + 0.3682745155601497 r + 4), E
       0.1907137600582818 r
     (E                     + 0.3814275201165636 r + 4), 
     0.0987195948597075 r   0.197439189719415 r
    E                     (E                    + 0.39487837943883 r
            0.1021574371047232 r   0.2043148742094465 r
     + 4), E                     (E
                                  0.1056710629744951 r
     + 0.408629748418893 r + 4), E
       0.2113421259489903 r
     (E                     + 0.4226842518979805 r + 4), 
     0.1092611211010309 r   0.2185222422020618 r
    E                     (E                     + 0.4370444844041237 r
            0.1129282524731764 r   0.2258565049463528 r
     + 4), E                     (E
                                   0.1166730903725168 r
     + 0.4517130098927056 r + 4), E
       0.2333461807450337 r
     (E                     + 0.4666923614900673 r + 4), 
     0.1204962603100498 r   0.2409925206200996 r
    E                     (E                     + 0.4819850412401991 r
            0.1243983799636342 r   0.2487967599272685 r
     + 4), E                     (E
                                   0.1283800591162231 r
     + 0.4975935198545369 r + 4), E
       0.2567601182324462 r
     (E                     + 0.5135202364648923 r + 4), 
     0.1324418995948859 r   0.2648837991897719 r
    E                     (E                     + 0.5297675983795438 r
            0.1365844952106265 r   0.2731689904212531 r
     + 4), E                     (E
                                   0.140808431699002 r
     + 0.5463379808425062 r + 4), E
       0.2816168633980041 r
     (E                     + 0.5632337267960081 r + 4), 
     0.1451142866615502 r   0.2902285733231005 r
    E                     (E                     + 0.580457146646201 r
            0.1495026295080298 r   0.2990052590160597 r
     + 4), E                     (E
                                   0.1539740213994798 r
     + 0.5980105180321194 r + 4), E
       0.3079480427989596 r
     (E                     + 0.6158960855979192 r + 4)]
    

\>plot2d(["f(x)","df(x)"],-pi,pi,color=[blue,red]), label("f(x)",2,0.6), label("df(x)",1,-0.5):


    Error : f(x) does not produce a real or column vector
    
    Error generated by error() command
    
    %ploteval:
        error(f$|" does not produce a real or column vector"); 
    adaptiveevalone:
        s=%ploteval(g$,t;args());
    Try "trace errors" to inspect local variables after errors.
    plot2d:
        dw/n,dw/n^2,dw/n,auto;args());

                                     2  

\>function f(x) &= log(3\*x+1)


    
            [0, log(4.999975000072321e-7 r + 1), 
    log(3.999920000760659e-6 r + 1), log(1.34993925130153e-5 r + 1), 
    log(3.199744009751981e-5 r + 1), log(6.249218796501588e-5 r + 1), 
    log(1.079805616662072e-4 r + 1), log(1.714579874017158e-4 r + 1), 
    log(2.559180924819188e-4 r + 1), log(3.643524059668696e-4 r + 1), 
    log(4.997500595155524e-4 r + 1), log(6.650974884755689e-4 r + 1), 
    log(8.633781332419016e-4 r + 1), log(0.001097572140915437 r + 1), 
    log(0.00137065606729056 r + 1), log(0.001685602579202333 r + 1), 
    log(0.002045380157262078 r + 1), log(0.002452952799011948 r + 1), 
    log(0.002911279722527443 r + 1), log(0.003423315070498284 r + 1), 
    log(0.003992007614816384 r + 1), log(0.00462030046170131 r + 1), 
    log(0.005311130757392035 r + 1), log(0.006067429394434803 r + 1), 
    log(0.00689212071859624 r + 1), log(0.007788122236431189 r + 1), 
    log(0.008758344323534673 r + 1), log(0.009805689933506612 r + 1), 
    log(0.01093305430765878 r + 1), log(0.01214332468549334 r + 1), 
    log(0.01343938001598133 r + 1), log(0.0148240906696695 r + 1), 
    log(0.01630031815164673 r + 1), log(0.01787091481539493 r + 1), 
    log(0.01953872357755687 r + 1), log(0.02130657763364591 r + 1), 
    log(0.02317730017473013 r + 1), log(0.02515370410511403 r + 1), 
    log(0.02723859176105198 r + 1), log(0.02943475463051576 r + 1), 
    log(0.0317449730740485 r + 1), log(0.03417201604673142 r + 1), 
    log(0.03671864082128951 r + 1), log(0.03938759271236769 r + 1), 
    log(0.04218160480200134 r + 1), log(0.0451033976663095 r + 1), 
    log(0.04815567910344071 r + 1), log(0.05134114386279526 r + 1), 
    log(0.05466247337555141 r + 1), log(0.05812233548652607 r + 1), 
    log(0.06172338418739115 r + 1), log(0.06546825935127759 r + 1), 
    log(0.06935958646878998 r + 1), log(0.07339997638545925 r + 1), 
    log(0.07759202504066087 r + 1), log(0.08193831320802247 r + 1), 
    log(0.08644140623734997 r + 1), log(0.09110385379809227 r + 1), 
    log(0.09592818962437955 r + 1), log(0.1009169312616489 r + 1), 
    log(0.1060725798148942 r + 1), log(0.1113976196985564 r + 1), 
    log(0.1168945183880851 r + 1), log(0.1225657261731915 r + 1), 
    log(0.128413675912824 r + 1), log(0.1344407827918814 r + 1), 
    log(0.1406494440796987 r + 1), log(0.1470420388903213 r + 1), 
    log(0.1536209279445947 r + 1), log(0.1603884533340966 r + 1), 
    log(0.1673469382869271 r + 1), log(0.1744986869353904 r + 1), 
    log(0.1818459840855809 r + 1), log(0.1893910949889066 r + 1), 
    log(0.1971362651155651 r + 1), log(0.205083719929998 r + 1), 
    log(0.2132356646683464 r + 1), log(0.2215942841179303 r + 1), 
    log(0.23016174239877 r + 1), log(0.238940182747177 r + 1), 
    log(0.2479317273014321 r + 1), log(0.2571384768895728 r + 1), 
    log(0.2665625108193128 r + 1), log(0.2762058866701123 r + 1), 
    log(0.2860706400874227 r + 1), log(0.2961587845791225 r + 1), 
    log(0.3064723113141697 r + 1), log(0.3170131889234854 r + 1), 
    log(0.3277833633030928 r + 1), log(0.3387847574195292 r + 1), 
    log(0.3500192711175505 r + 1), log(0.3614887809301494 r + 1), 
    log(0.3731951398909027 r + 1), log(0.3851401773486692 r + 1), 
    log(0.3973256987846578 r + 1), log(0.4097534856318796 r + 1), 
    log(0.4224252950970061 r + 1), log(0.4353428599846507 r + 1), 
    log(0.4485078885240895 r + 1), log(0.4619220641984394 r + 1)]
    

\>$showev('limit((log(3\*x+h+1)-log(3\*x+1))/h,h,0))


$$\lim_{h\rightarrow 0}{\left[ \frac{\log \left(h+1\right)}{h} , 
 \frac{\log \left(4.999975000072321 \times 10^{-7}\,r+h+1\right)-
 \log \left(4.999975000072321 \times 10^{-7}\,r+1\right)}{h} , \frac{
 \log \left(3.999920000760659 \times 10^{-6}\,r+h+1\right)-\log 
 \left(3.999920000760659 \times 10^{-6}\,r+1\right)}{h} , \frac{\log 
 \left(1.34993925130153 \times 10^{-5}\,r+h+1\right)-\log \left(
 1.34993925130153 \times 10^{-5}\,r+1\right)}{h} , \frac{\log \left(
 3.199744009751981 \times 10^{-5}\,r+h+1\right)-\log \left(
 3.199744009751981 \times 10^{-5}\,r+1\right)}{h} , \frac{\log \left(
 6.249218796501588 \times 10^{-5}\,r+h+1\right)-\log \left(
 6.249218796501588 \times 10^{-5}\,r+1\right)}{h} , \frac{\log \left(
 1.079805616662072 \times 10^{-4}\,r+h+1\right)-\log \left(
 1.079805616662072 \times 10^{-4}\,r+1\right)}{h} , \frac{\log \left(
 1.714579874017158 \times 10^{-4}\,r+h+1\right)-\log \left(
 1.714579874017158 \times 10^{-4}\,r+1\right)}{h} , \frac{\log \left(
 2.559180924819188 \times 10^{-4}\,r+h+1\right)-\log \left(
 2.559180924819188 \times 10^{-4}\,r+1\right)}{h} , \frac{\log \left(
 3.643524059668696 \times 10^{-4}\,r+h+1\right)-\log \left(
 3.643524059668696 \times 10^{-4}\,r+1\right)}{h} , \frac{\log \left(
 4.997500595155524 \times 10^{-4}\,r+h+1\right)-\log \left(
 4.997500595155524 \times 10^{-4}\,r+1\right)}{h} , \frac{\log \left(
 6.650974884755689 \times 10^{-4}\,r+h+1\right)-\log \left(
 6.650974884755689 \times 10^{-4}\,r+1\right)}{h} , \frac{\log \left(
 8.633781332419016 \times 10^{-4}\,r+h+1\right)-\log \left(
 8.633781332419016 \times 10^{-4}\,r+1\right)}{h} , \frac{\log \left(
 0.001097572140915437\,r+h+1\right)-\log \left(0.001097572140915437\,
 r+1\right)}{h} , \frac{\log \left(0.00137065606729056\,r+h+1\right)-
 \log \left(0.00137065606729056\,r+1\right)}{h} , \frac{\log \left(
 0.001685602579202333\,r+h+1\right)-\log \left(0.001685602579202333\,
 r+1\right)}{h} , \frac{\log \left(0.002045380157262078\,r+h+1\right)
 -\log \left(0.002045380157262078\,r+1\right)}{h} , \frac{\log \left(
 0.002452952799011948\,r+h+1\right)-\log \left(0.002452952799011948\,
 r+1\right)}{h} , \frac{\log \left(0.002911279722527443\,r+h+1\right)
 -\log \left(0.002911279722527443\,r+1\right)}{h} , \frac{\log \left(
 0.003423315070498284\,r+h+1\right)-\log \left(0.003423315070498284\,
 r+1\right)}{h} , \frac{\log \left(0.003992007614816384\,r+h+1\right)
 -\log \left(0.003992007614816384\,r+1\right)}{h} , \frac{\log \left(
 0.00462030046170131\,r+h+1\right)-\log \left(0.00462030046170131\,r+
 1\right)}{h} , \frac{\log \left(0.005311130757392035\,r+h+1\right)-
 \log \left(0.005311130757392035\,r+1\right)}{h} , \frac{\log \left(
 0.006067429394434803\,r+h+1\right)-\log \left(0.006067429394434803\,
 r+1\right)}{h} , \frac{\log \left(0.00689212071859624\,r+h+1\right)-
 \log \left(0.00689212071859624\,r+1\right)}{h} , \frac{\log \left(
 0.007788122236431189\,r+h+1\right)-\log \left(0.007788122236431189\,
 r+1\right)}{h} , \frac{\log \left(0.008758344323534673\,r+h+1\right)
 -\log \left(0.008758344323534673\,r+1\right)}{h} , \frac{\log \left(
 0.009805689933506612\,r+h+1\right)-\log \left(0.009805689933506612\,
 r+1\right)}{h} , \frac{\log \left(0.01093305430765878\,r+h+1\right)-
 \log \left(0.01093305430765878\,r+1\right)}{h} , \frac{\log \left(
 0.01214332468549334\,r+h+1\right)-\log \left(0.01214332468549334\,r+
 1\right)}{h} , \frac{\log \left(0.01343938001598133\,r+h+1\right)-
 \log \left(0.01343938001598133\,r+1\right)}{h} , \frac{\log \left(
 0.0148240906696695\,r+h+1\right)-\log \left(0.0148240906696695\,r+1
 \right)}{h} , \frac{\log \left(0.01630031815164673\,r+h+1\right)-
 \log \left(0.01630031815164673\,r+1\right)}{h} , \frac{\log \left(
 0.01787091481539493\,r+h+1\right)-\log \left(0.01787091481539493\,r+
 1\right)}{h} , \frac{\log \left(0.01953872357755687\,r+h+1\right)-
 \log \left(0.01953872357755687\,r+1\right)}{h} , \frac{\log \left(
 0.02130657763364591\,r+h+1\right)-\log \left(0.02130657763364591\,r+
 1\right)}{h} , \frac{\log \left(0.02317730017473013\,r+h+1\right)-
 \log \left(0.02317730017473013\,r+1\right)}{h} , \frac{\log \left(
 0.02515370410511403\,r+h+1\right)-\log \left(0.02515370410511403\,r+
 1\right)}{h} , \frac{\log \left(0.02723859176105198\,r+h+1\right)-
 \log \left(0.02723859176105198\,r+1\right)}{h} , \frac{\log \left(
 0.02943475463051576\,r+h+1\right)-\log \left(0.02943475463051576\,r+
 1\right)}{h} , \frac{\log \left(0.0317449730740485\,r+h+1\right)-
 \log \left(0.0317449730740485\,r+1\right)}{h} , \frac{\log \left(
 0.03417201604673142\,r+h+1\right)-\log \left(0.03417201604673142\,r+
 1\right)}{h} , \frac{\log \left(0.03671864082128951\,r+h+1\right)-
 \log \left(0.03671864082128951\,r+1\right)}{h} , \frac{\log \left(
 0.03938759271236769\,r+h+1\right)-\log \left(0.03938759271236769\,r+
 1\right)}{h} , \frac{\log \left(0.04218160480200134\,r+h+1\right)-
 \log \left(0.04218160480200134\,r+1\right)}{h} , \frac{\log \left(
 0.0451033976663095\,r+h+1\right)-\log \left(0.0451033976663095\,r+1
 \right)}{h} , \frac{\log \left(0.04815567910344071\,r+h+1\right)-
 \log \left(0.04815567910344071\,r+1\right)}{h} , \frac{\log \left(
 0.05134114386279526\,r+h+1\right)-\log \left(0.05134114386279526\,r+
 1\right)}{h} , \frac{\log \left(0.05466247337555141\,r+h+1\right)-
 \log \left(0.05466247337555141\,r+1\right)}{h} , \frac{\log \left(
 0.05812233548652607\,r+h+1\right)-\log \left(0.05812233548652607\,r+
 1\right)}{h} , \frac{\log \left(0.06172338418739115\,r+h+1\right)-
 \log \left(0.06172338418739115\,r+1\right)}{h} , \frac{\log \left(
 0.06546825935127759\,r+h+1\right)-\log \left(0.06546825935127759\,r+
 1\right)}{h} , \frac{\log \left(0.06935958646878998\,r+h+1\right)-
 \log \left(0.06935958646878998\,r+1\right)}{h} , \frac{\log \left(
 0.07339997638545925\,r+h+1\right)-\log \left(0.07339997638545925\,r+
 1\right)}{h} , \frac{\log \left(0.07759202504066087\,r+h+1\right)-
 \log \left(0.07759202504066087\,r+1\right)}{h} , \frac{\log \left(
 0.08193831320802247\,r+h+1\right)-\log \left(0.08193831320802247\,r+
 1\right)}{h} , \frac{\log \left(0.08644140623734997\,r+h+1\right)-
 \log \left(0.08644140623734997\,r+1\right)}{h} , \frac{\log \left(
 0.09110385379809227\,r+h+1\right)-\log \left(0.09110385379809227\,r+
 1\right)}{h} , \frac{\log \left(0.09592818962437955\,r+h+1\right)-
 \log \left(0.09592818962437955\,r+1\right)}{h} , \frac{\log \left(
 0.1009169312616489\,r+h+1\right)-\log \left(0.1009169312616489\,r+1
 \right)}{h} , \frac{\log \left(0.1060725798148942\,r+h+1\right)-
 \log \left(0.1060725798148942\,r+1\right)}{h} , \frac{\log \left(
 0.1113976196985564\,r+h+1\right)-\log \left(0.1113976196985564\,r+1
 \right)}{h} , \frac{\log \left(0.1168945183880851\,r+h+1\right)-
 \log \left(0.1168945183880851\,r+1\right)}{h} , \frac{\log \left(
 0.1225657261731915\,r+h+1\right)-\log \left(0.1225657261731915\,r+1
 \right)}{h} , \frac{\log \left(0.128413675912824\,r+h+1\right)-\log 
 \left(0.128413675912824\,r+1\right)}{h} , \frac{\log \left(
 0.1344407827918814\,r+h+1\right)-\log \left(0.1344407827918814\,r+1
 \right)}{h} , \frac{\log \left(0.1406494440796987\,r+h+1\right)-
 \log \left(0.1406494440796987\,r+1\right)}{h} , \frac{\log \left(
 0.1470420388903213\,r+h+1\right)-\log \left(0.1470420388903213\,r+1
 \right)}{h} , \frac{\log \left(0.1536209279445947\,r+h+1\right)-
 \log \left(0.1536209279445947\,r+1\right)}{h} , \frac{\log \left(
 0.1603884533340966\,r+h+1\right)-\log \left(0.1603884533340966\,r+1
 \right)}{h} , \frac{\log \left(0.1673469382869271\,r+h+1\right)-
 \log \left(0.1673469382869271\,r+1\right)}{h} , \frac{\log \left(
 0.1744986869353904\,r+h+1\right)-\log \left(0.1744986869353904\,r+1
 \right)}{h} , \frac{\log \left(0.1818459840855809\,r+h+1\right)-
 \log \left(0.1818459840855809\,r+1\right)}{h} , \frac{\log \left(
 0.1893910949889066\,r+h+1\right)-\log \left(0.1893910949889066\,r+1
 \right)}{h} , \frac{\log \left(0.1971362651155651\,r+h+1\right)-
 \log \left(0.1971362651155651\,r+1\right)}{h} , \frac{\log \left(
 0.205083719929998\,r+h+1\right)-\log \left(0.205083719929998\,r+1
 \right)}{h} , \frac{\log \left(0.2132356646683464\,r+h+1\right)-
 \log \left(0.2132356646683464\,r+1\right)}{h} , \frac{\log \left(
 0.2215942841179303\,r+h+1\right)-\log \left(0.2215942841179303\,r+1
 \right)}{h} , \frac{\log \left(0.23016174239877\,r+h+1\right)-\log 
 \left(0.23016174239877\,r+1\right)}{h} , \frac{\log \left(
 0.238940182747177\,r+h+1\right)-\log \left(0.238940182747177\,r+1
 \right)}{h} , \frac{\log \left(0.2479317273014321\,r+h+1\right)-
 \log \left(0.2479317273014321\,r+1\right)}{h} , \frac{\log \left(
 0.2571384768895728\,r+h+1\right)-\log \left(0.2571384768895728\,r+1
 \right)}{h} , \frac{\log \left(0.2665625108193128\,r+h+1\right)-
 \log \left(0.2665625108193128\,r+1\right)}{h} , \frac{\log \left(
 0.2762058866701123\,r+h+1\right)-\log \left(0.2762058866701123\,r+1
 \right)}{h} , \frac{\log \left(0.2860706400874227\,r+h+1\right)-
 \log \left(0.2860706400874227\,r+1\right)}{h} , \frac{\log \left(
 0.2961587845791225\,r+h+1\right)-\log \left(0.2961587845791225\,r+1
 \right)}{h} , \frac{\log \left(0.3064723113141697\,r+h+1\right)-
 \log \left(0.3064723113141697\,r+1\right)}{h} , \frac{\log \left(
 0.3170131889234854\,r+h+1\right)-\log \left(0.3170131889234854\,r+1
 \right)}{h} , \frac{\log \left(0.3277833633030928\,r+h+1\right)-
 \log \left(0.3277833633030928\,r+1\right)}{h} , \frac{\log \left(
 0.3387847574195292\,r+h+1\right)-\log \left(0.3387847574195292\,r+1
 \right)}{h} , \frac{\log \left(0.3500192711175505\,r+h+1\right)-
 \log \left(0.3500192711175505\,r+1\right)}{h} , \frac{\log \left(
 0.3614887809301494\,r+h+1\right)-\log \left(0.3614887809301494\,r+1
 \right)}{h} , \frac{\log \left(0.3731951398909027\,r+h+1\right)-
 \log \left(0.3731951398909027\,r+1\right)}{h} , \frac{\log \left(
 0.3851401773486692\,r+h+1\right)-\log \left(0.3851401773486692\,r+1
 \right)}{h} , \frac{\log \left(0.3973256987846578\,r+h+1\right)-
 \log \left(0.3973256987846578\,r+1\right)}{h} , \frac{\log \left(
 0.4097534856318796\,r+h+1\right)-\log \left(0.4097534856318796\,r+1
 \right)}{h} , \frac{\log \left(0.4224252950970061\,r+h+1\right)-
 \log \left(0.4224252950970061\,r+1\right)}{h} , \frac{\log \left(
 0.4353428599846507\,r+h+1\right)-\log \left(0.4353428599846507\,r+1
 \right)}{h} , \frac{\log \left(0.4485078885240895\,r+h+1\right)-
 \log \left(0.4485078885240895\,r+1\right)}{h} , \frac{\log \left(
 0.4619220641984394\,r+h+1\right)-\log \left(0.4619220641984394\,r+1
 \right)}{h} \right] }=\left[ 1 , \frac{94914474571}{47457\,r+
 94914474571} , \frac{9531440627}{38125\,r+9531440627} , \frac{
 5341573699}{72108\,r+5341573699} , \frac{4922049999}{157493\,r+
 4922049999} , \frac{1710693824}{106905\,r+1710693824} , \frac{
 2346274145}{253352\,r+2346274145} , \frac{298347139}{51154\,r+
 298347139} , \frac{475507608}{121691\,r+475507608} , \frac{
 1243200244}{452963\,r+1243200244} , \frac{855553675}{427563\,r+
 855553675} , \frac{809975995}{538713\,r+809975995} , \frac{
 1352516302}{1167733\,r+1352516302} , \frac{1237730031}{1358498\,r+
 1237730031} , \frac{191862865}{262978\,r+191862865} , \frac{
 268025812}{451785\,r+268025812} , \frac{94024575}{192316\,r+94024575
 } , \frac{129445214}{317523\,r+129445214} , \frac{225343513}{656038
 \,r+225343513} , \frac{420072056}{1438039\,r+420072056} , \frac{
 340981564}{1361201\,r+340981564} , \frac{179783113}{830652\,r+
 179783113} , \frac{121328024}{644389\,r+121328024} , \frac{222924885
 }{1352581\,r+222924885} , \frac{221766429}{1528441\,r+221766429} , 
 \frac{303907531}{2366869\,r+303907531} , \frac{103469442}{906221\,r+
 103469442} , \frac{237014123}{2324087\,r+237014123} , \frac{
 1637212301}{17899731\,r+1637212301} , \frac{141417202}{1717275\,r+
 141417202} , \frac{188791447}{2537240\,r+188791447} , \frac{
 214572217}{3180838\,r+214572217} , \frac{311759191}{5081774\,r+
 311759191} , \frac{242979503}{4342266\,r+242979503} , \frac{
 175681947}{3432601\,r+175681947} , \frac{94977196}{2023639\,r+
 94977196} , \frac{189545459}{4393152\,r+189545459} , \frac{132814117
 }{3340767\,r+132814117} , \frac{15929825}{433906\,r+15929825} , 
 \frac{138926587}{4089270\,r+138926587} , \frac{36658686}{1163729\,r+
 36658686} , \frac{385089015}{13159268\,r+385089015} , \frac{
 186534764}{6849303\,r+186534764} , \frac{288805185}{11375341\,r+
 288805185} , \frac{129469517}{5461232\,r+129469517} , \frac{13335359
 }{601470\,r+13335359} , \frac{59305840}{2855913\,r+59305840} , 
 \frac{593184797}{30454786\,r+593184797} , \frac{81896532}{4476667\,r
 +81896532} , \frac{104199839}{6056338\,r+104199839} , \frac{95358041
 }{5885821\,r+95358041} , \frac{342548087}{22426027\,r+342548087} , 
 \frac{86945602}{6030511\,r+86945602} , \frac{55787661}{4094813\,r+
 55787661} , \frac{52004378}{4035125\,r+52004378} , \frac{31428997}{
 2575239\,r+31428997} , \frac{130310918}{11264259\,r+130310918} , 
 \frac{97283327}{8862886\,r+97283327} , \frac{36461472}{3497683\,r+
 36461472} , \frac{83699622}{8446709\,r+83699622} , \frac{51353479}{
 5447196\,r+51353479} , \frac{69200563}{7708778\,r+69200563} , \frac{
 61735983}{7216598\,r+61735983} , \frac{91201377}{11178163\,r+
 91201377} , \frac{78253877}{10048868\,r+78253877} , \frac{148311298
 }{19939087\,r+148311298} , \frac{80354324}{11301791\,r+80354324} , 
 \frac{75953551}{11168365\,r+75953551} , \frac{56637153}{8700652\,r+
 56637153} , \frac{74808677}{11998448\,r+74808677} , \frac{8354016}{
 1398019\,r+8354016} , \frac{40804542}{7120339\,r+40804542} , \frac{
 35409146}{6439011\,r+35409146} , \frac{77360802}{14651447\,r+
 77360802} , \frac{21509533}{4240309\,r+21509533} , \frac{39739522}{
 8149929\,r+39739522} , \frac{44270357}{9440019\,r+44270357} , \frac{
 184692124}{40926719\,r+184692124} , \frac{70798443}{16295093\,r+
 70798443} , \frac{62385095}{14906306\,r+62385095} , \frac{76537417}{
 18976054\,r+76537417} , \frac{41837111}{10757931\,r+41837111} , 
 \frac{21576001}{5751353\,r+21576001} , \frac{79347983}{21916380\,r+
 79347983} , \frac{82430787}{23581028\,r+82430787} , \frac{28234631}{
 8361934\,r+28234631} , \frac{81603584}{25009239\,r+81603584} , 
 \frac{71653839}{22715212\,r+71653839} , \frac{16937629}{5551873\,r+
 16937629} , \frac{34088585}{11548693\,r+34088585} , \frac{31321484}{
 10963123\,r+31321484} , \frac{52663947}{19037426\,r+52663947} , 
 \frac{21346599}{7966447\,r+21346599} , \frac{6203035}{2389038\,r+
 6203035} , \frac{49943140}{19843693\,r+49943140} , \frac{4487852}{
 1838913\,r+4487852} , \frac{28305438}{11956933\,r+28305438} , \frac{
 24491572}{10662231\,r+24491572} , \frac{59662935}{26759297\,r+
 59662935} , \frac{97403271}{44992720\,r+97403271} \right] $$\>function df(x) &= limit(((log(3\*x+h+1)-log(3\*x+1))/h) ,h,0);  $df(x)// df(x) = f'(x)


$$\left[ 1 , \frac{94914474571}{47457\,r+94914474571} , \frac{
 9531440627}{38125\,r+9531440627} , \frac{5341573699}{72108\,r+
 5341573699} , \frac{4922049999}{157493\,r+4922049999} , \frac{
 1710693824}{106905\,r+1710693824} , \frac{2346274145}{253352\,r+
 2346274145} , \frac{298347139}{51154\,r+298347139} , \frac{475507608
 }{121691\,r+475507608} , \frac{1243200244}{452963\,r+1243200244} , 
 \frac{855553675}{427563\,r+855553675} , \frac{809975995}{538713\,r+
 809975995} , \frac{1352516302}{1167733\,r+1352516302} , \frac{
 1237730031}{1358498\,r+1237730031} , \frac{191862865}{262978\,r+
 191862865} , \frac{268025812}{451785\,r+268025812} , \frac{94024575
 }{192316\,r+94024575} , \frac{129445214}{317523\,r+129445214} , 
 \frac{225343513}{656038\,r+225343513} , \frac{420072056}{1438039\,r+
 420072056} , \frac{340981564}{1361201\,r+340981564} , \frac{
 179783113}{830652\,r+179783113} , \frac{121328024}{644389\,r+
 121328024} , \frac{222924885}{1352581\,r+222924885} , \frac{
 221766429}{1528441\,r+221766429} , \frac{303907531}{2366869\,r+
 303907531} , \frac{103469442}{906221\,r+103469442} , \frac{237014123
 }{2324087\,r+237014123} , \frac{1637212301}{17899731\,r+1637212301}
  , \frac{141417202}{1717275\,r+141417202} , \frac{188791447}{2537240
 \,r+188791447} , \frac{214572217}{3180838\,r+214572217} , \frac{
 311759191}{5081774\,r+311759191} , \frac{242979503}{4342266\,r+
 242979503} , \frac{175681947}{3432601\,r+175681947} , \frac{94977196
 }{2023639\,r+94977196} , \frac{189545459}{4393152\,r+189545459} , 
 \frac{132814117}{3340767\,r+132814117} , \frac{15929825}{433906\,r+
 15929825} , \frac{138926587}{4089270\,r+138926587} , \frac{36658686
 }{1163729\,r+36658686} , \frac{385089015}{13159268\,r+385089015} , 
 \frac{186534764}{6849303\,r+186534764} , \frac{288805185}{11375341\,
 r+288805185} , \frac{129469517}{5461232\,r+129469517} , \frac{
 13335359}{601470\,r+13335359} , \frac{59305840}{2855913\,r+59305840}
  , \frac{593184797}{30454786\,r+593184797} , \frac{81896532}{4476667
 \,r+81896532} , \frac{104199839}{6056338\,r+104199839} , \frac{
 95358041}{5885821\,r+95358041} , \frac{342548087}{22426027\,r+
 342548087} , \frac{86945602}{6030511\,r+86945602} , \frac{55787661}{
 4094813\,r+55787661} , \frac{52004378}{4035125\,r+52004378} , \frac{
 31428997}{2575239\,r+31428997} , \frac{130310918}{11264259\,r+
 130310918} , \frac{97283327}{8862886\,r+97283327} , \frac{36461472}{
 3497683\,r+36461472} , \frac{83699622}{8446709\,r+83699622} , \frac{
 51353479}{5447196\,r+51353479} , \frac{69200563}{7708778\,r+69200563
 } , \frac{61735983}{7216598\,r+61735983} , \frac{91201377}{11178163
 \,r+91201377} , \frac{78253877}{10048868\,r+78253877} , \frac{
 148311298}{19939087\,r+148311298} , \frac{80354324}{11301791\,r+
 80354324} , \frac{75953551}{11168365\,r+75953551} , \frac{56637153}{
 8700652\,r+56637153} , \frac{74808677}{11998448\,r+74808677} , 
 \frac{8354016}{1398019\,r+8354016} , \frac{40804542}{7120339\,r+
 40804542} , \frac{35409146}{6439011\,r+35409146} , \frac{77360802}{
 14651447\,r+77360802} , \frac{21509533}{4240309\,r+21509533} , 
 \frac{39739522}{8149929\,r+39739522} , \frac{44270357}{9440019\,r+
 44270357} , \frac{184692124}{40926719\,r+184692124} , \frac{70798443
 }{16295093\,r+70798443} , \frac{62385095}{14906306\,r+62385095} , 
 \frac{76537417}{18976054\,r+76537417} , \frac{41837111}{10757931\,r+
 41837111} , \frac{21576001}{5751353\,r+21576001} , \frac{79347983}{
 21916380\,r+79347983} , \frac{82430787}{23581028\,r+82430787} , 
 \frac{28234631}{8361934\,r+28234631} , \frac{81603584}{25009239\,r+
 81603584} , \frac{71653839}{22715212\,r+71653839} , \frac{16937629}{
 5551873\,r+16937629} , \frac{34088585}{11548693\,r+34088585} , 
 \frac{31321484}{10963123\,r+31321484} , \frac{52663947}{19037426\,r+
 52663947} , \frac{21346599}{7966447\,r+21346599} , \frac{6203035}{
 2389038\,r+6203035} , \frac{49943140}{19843693\,r+49943140} , \frac{
 4487852}{1838913\,r+4487852} , \frac{28305438}{11956933\,r+28305438}
  , \frac{24491572}{10662231\,r+24491572} , \frac{59662935}{26759297
 \,r+59662935} , \frac{97403271}{44992720\,r+97403271} \right] $$# Integral

EMT dapat digunakan untuk menghitung integral, baik integral tak tentu
maupun integral tentu. Untuk integral tak tentu (simbolik) sudah tentu
EMT menggunakan Maxima, sedangkan untuk perhitungan integral tentu EMT
sudah menyediakan beberapa fungsi yang mengimplementasikan algoritma
kuadratur (perhitungan integral tentu menggunakan metode numerik).


Pada notebook ini akan ditunjukkan perhitungan integral tentu dengan
menggunakan Teorema Dasar Kalkulus:


$$\int_a^b f(x)\ dx = F(b)-F(a), \quad \text{ dengan  } F'(x) = f(x).$$Fungsi untuk menentukan integral adalah integrate. Fungsi ini dapat
digunakan untuk menentukan, baik integral tentu maupun tak tentu (jika
fungsinya memiliki antiderivatif). Untuk perhitungan integral tentu
fungsi integrate menggunakan metode numerik (kecuali fungsinya tidak
integrabel, kita tidak akan menggunakan metode ini).


\>$showev('integrate(x^n,x))


    
    Maxima output too long!
    Error in:
    $showev('integrate(x^n,x)) ...
                              ^

\>$showev('integrate(1/(1+x),x))


    
    Maxima output too long!
    Error in:
    $showev('integrate(1/(1+x),x)) ...
                                  ^

\>$showev('integrate(1/(1+x^2),x))


$$\int {\frac{1}{x^2+1}}{\;dx}=\arctan x$$\>$showev('integrate(1/sqrt(1-x^2),x))


$$\int {\frac{1}{\sqrt{1-x^2}}}{\;dx}=\arcsin x$$\>$showev('integrate(sin(x),x,0,pi))


$$\int_{0}^{\pi}{\sin x\;dx}=2$$\>plot2d("sin(x)",0,2\*pi):


![images/EMT4Kalkulus%20(1)-198.png](images/EMT4Kalkulus%20(1)-198.png)

\>$showev('integrate(sin(x),x,a,b))


$$\int_{a}^{b}{\sin x\;dx}=\cos a-\cos b$$\>$showev('integrate(x^n,x,a,b))


    Answering "Is n positive, negative or zero?" with "positive"

$$\int_{a}^{b}{x^{n}\;dx}=\frac{b^{n+1}}{n+1}-\frac{a^{n+1}}{n+1}$$\>$showev('integrate(x^2\*sqrt(2\*x+1),x))


$$\int {x^2\,\sqrt{2\,x+1}}{\;dx}=\frac{\left(2\,x+1\right)^{\frac{7
 }{2}}}{28}-\frac{\left(2\,x+1\right)^{\frac{5}{2}}}{10}+\frac{\left(
 2\,x+1\right)^{\frac{3}{2}}}{12}$$\>$showev('integrate(x^2\*sqrt(2\*x+1),x,0,2))


$$\int_{0}^{2}{x^2\,\sqrt{2\,x+1}\;dx}=\frac{2\,5^{\frac{5}{2}}}{21}-
 \frac{2}{105}$$\>$ratsimp(%)


$$\int_{0}^{2}{x^2\,\sqrt{2\,x+1}\;dx}=\frac{2\,5^{\frac{7}{2}}-2}{
 105}$$\>$showev('integrate((sin(sqrt(x)+a)\*E^sqrt(x))/sqrt(x),x,0,pi^2))


$$\int_{0}^{\pi^2}{\frac{\sin \left(\sqrt{x}+a\right)\,e^{\sqrt{x}}}{
 \sqrt{x}}\;dx}=\left(-e^{\pi}-1\right)\,\sin a+\left(e^{\pi}+1
 \right)\,\cos a$$\>$factor(%)


$$\int_{0}^{\pi^2}{\frac{\sin \left(\sqrt{x}+a\right)\,e^{\sqrt{x}}}{
 \sqrt{x}}\;dx}=\left(-e^{\pi}-1\right)\,\left(\sin a-\cos a\right)$$\>function map f(x) &= E^(-x^2)


    
                                        2
                                     - x
                                    E
    

\>$showev('integrate(f(x),x))


$$\int {e^ {- x^2 }}{\;dx}=\frac{\sqrt{\pi}\,\mathrm{erf}\left(x
 \right)}{2}$$Fungsi f tidak memiliki antiturunan, integralnya masih memuat integral
lain.


$$erf(x) = \int \frac{e^{-x^2}}{\sqrt{\pi}} \ dx.$$Kita tidak dapat menggunakan teorema Dasar kalkulus untuk menghitung
integral tentu fungsi tersebut jika semua batasnya berhingga. Dalam
hal ini dapat digunakan metode numerik (rumus kuadratur).


Misalkan kita akan menghitung:


$$\int_{0}^{\pi}{e^ {- x^2 }\;dx}$$\>x=0:0.1:pi-0.1; plot2d(x,f(x+0.1),\>bar); plot2d("f(x)",0,pi,\>add):


![images/EMT4Kalkulus%20(1)-209.png](images/EMT4Kalkulus%20(1)-209.png)

Integral tentu


$$\int_{0}^{\pi}{e^ {- x^2 }\;dx}$$dapat dihampiri dengan jumlah luas persegi-persegi panjang di bawah
kurva y=f(x) tersebut. Langkah-langkahnya adalah sebagai berikut.


\>t &= makelist(a,a,0,pi-0.1,0.1); // t sebagai list untuk menyimpan nilai-nilai x

\>fx &= makelist(f(t[i]+0.1),i,1,length(t)); // simpan nilai-nilai f(x)

\>// jangan menggunakan x sebagai list, kecuali Anda pakar Maxima!


Hasilnya adalah:


$$\int_{0}^{\pi}{e^ {- x^2 }\;dx}=0.8362196102528469$$Jumlah tersebut diperoleh dari hasil kali lebar sub-subinterval (=0.1)
dan jumlah nilai-nilai f(x) untuk x = 0.1, 0.2, 0.3, ..., 3.2.


\>0.1\*sum(f(x+0.1)) // cek langsung dengan perhitungan numerik EMT


    0.836219610253

Untuk mendapatkan nilai integral tentu yang mendekati nilai sebenarnya, lebar
sub-intervalnya dapat diperkecil lagi, sehingga daerah di bawah kurva tertutup
semuanya, misalnya dapat digunakan lebar subinterval 0.001. (Silakan dicoba!)


Meskipun Maxima tidak dapat menghitung integral tentu fungsi tersebut untuk
batas-batas yang berhingga, namun integral tersebut dapat dihitung secara eksak jika
batas-batasnya tak hingga. Ini adalah salah satu keajaiban di dalam matematika, yang
terbatas tidak dapat dihitung secara eksak, namun yang tak hingga malah dapat
dihitung secara eksak.


\>$showev('integrate(f(x),x,0,inf))


$$\int_{0}^{\infty }{e^ {- x^2 }\;dx}=\frac{\sqrt{\pi}}{2}$$Tunjukkan kebenaran hasil di atas!


Berikut adalah contoh lain fungsi yang tidak memiliki antiderivatif, sehingga integral tentunya hanya
dapat dihitung dengan metode numerik.


\>function f(x) &= x^x


    
                                       x
                                      x
    

\>$showev('integrate(f(x),x,0,1))


$$\int_{0}^{1}{x^{x}\;dx}=\int_{0}^{1}{x^{x}\;dx}$$\>x=0:0.1:1-0.01; plot2d(x,f(x+0.01),\>bar); plot2d("f(x)",0,1,\>add):


![images/EMT4Kalkulus%20(1)-214.png](images/EMT4Kalkulus%20(1)-214.png)

Maxima gagal menghitung integral tentu tersebut secara langsung menggunakan perintah
integrate. Berikut kita lakukan seperti contoh sebelumnya untuk mendapat hasil atau
pendekatan nilai integral tentu tersebut.


\>t &= makelist(a,a,0,1-0.01,0.01);

\>fx &= makelist(f(t[i]+0.01),i,1,length(t));


$$\int_{0}^{1}{x^{x}\;dx}=0.7834935879025506$$Apakah hasil tersebut cukup baik? perhatikan gambarnya.


\>function f(x) &= sin(3\*x^5+7)^2


    
                                   2    5
                                sin (3 x  + 7)
    

\>integrate(f,0,1)


    0.542581176074

\>&showev('integrate(f(x),x,0,1))


    
             1                           1              pi
            /                      gamma(-) sin(14) sin(--)
            [     2    5                 5              10
            I  sin (3 x  + 7) dx = ------------------------
            ]                                  1/5
            /                              10 6
             0
           4/5                  1          4/5                  1
     - (((6    gamma_incomplete(-, 6 I) + 6    gamma_incomplete(-, - 6 I))
                                5                               5
                 4/5                    1
     sin(14) + (6    I gamma_incomplete(-, 6 I)
                                        5
        4/5                    1                       pi
     - 6    I gamma_incomplete(-, - 6 I)) cos(14)) sin(--) - 60)/120
                               5                       10
    

\>&float(%)


    
             1.0
            /
            [       2      5
            I    sin (3.0 x  + 7.0) dx = 
            ]
            /
             0.0
    0.09820784258795788 - 0.008333333333333333
     (0.3090169943749474 (0.1367372182078336
     (4.192962712629476 I gamma__incomplete(0.2, 6.0 I)
     - 4.192962712629476 I gamma__incomplete(0.2, - 6.0 I))
     + 0.9906073556948704 (4.192962712629476 gamma__incomplete(0.2, 6.0 I)
     + 4.192962712629476 gamma__incomplete(0.2, - 6.0 I))) - 60.0)
    

\>$showev('integrate(x\*exp(-x),x,0,1)) // Integral tentu (eksak)


$$\int_{0}^{1}{x\,e^ {- x }\;dx}=1-2\,e^ {- 1 }$$# Aplikasi Integral Tentu

\>plot2d("x^3-x",-0.1,1.1); plot2d("-x^2",\>add);  ...  
\>   b=solve("x^3-x+x^2",0.5); x=linspace(0,b,200); xi=flipx(x); ...  
\>   plot2d(x|xi,x^3-x|-xi^2,\>filled,style="|",fillcolor=1,\>add): // Plot daerah antara 2 kurva


![images/EMT4Kalkulus%20(1)-217.png](images/EMT4Kalkulus%20(1)-217.png)

\>a=solve("x^3-x+x^2",0), b=solve("x^3-x+x^2",1) // absis titik-titik potong kedua kurva


    0
    0.61803398875

\>integrate("(-x^2)-(x^3-x)",a,b) // luas daerah yang diarsir


    0.0758191713542

Hasil tersebut akan kita bandingkan dengan perhitungan secara analitik.


\>a &= solve((-x^2)-(x^3-x),x); $a // menentukan absis titik potong kedua kurva secara eksak


$$\left[ x=\frac{-\sqrt{5}-1}{2} , x=\frac{\sqrt{5}-1}{2} , x=0
  \right] $$\>$showev('integrate(-x^2-x^3+x,x,0,(sqrt(5)-1)/2)) // Nilai integral secara eksak


$$\int_{0}^{\frac{\sqrt{5}-1}{2}}{-x^3-x^2+x\;dx}=\frac{13-5^{\frac{3
 }{2}}}{24}$$\>$float(%)


$$\int_{0.0}^{0.6180339887498949}{-1.0\,x^3-1.0\,x^2+x\;dx}=
 0.07581917135421037$$## Panjang Kurva

Hitunglah panjang kurva berikut ini dan luas daerah di dalam kurva
tersebut.


$$\gamma(t) = (r(t) \cos(t), r(t) \sin(t))$$dengan


$$r(t) = 1 + \dfrac{\sin(3t)}{2},\quad 0\le t\le 2\pi.$$\>t=linspace(0,2pi,1000); r=1+sin(3\*t)/2; x=r\*cos(t); y=r\*sin(t); ...  
\>   plot2d(x,y,\>filled,fillcolor=red,style="/",r=1.5): // Kita gambar kurvanya terlebih dahulu


![images/EMT4Kalkulus%20(1)-223.png](images/EMT4Kalkulus%20(1)-223.png)

\>function r(t) &= 1+sin(3\*t)/2; $'r(t)=r(t)


$$r\left(\left[ 0 , 0.01 , 0.02 , 0.03 , 0.04 , 0.05 , 0.06 , 0.07 , 
 0.08 , 0.09 , 0.1 , 0.11 , 0.12 , 0.13 , 0.14 , 0.15 , 0.16 , 0.17
  , 0.18 , 0.19 , 0.2 , 0.21 , 0.2200000000000001 , 
 0.2300000000000001 , 0.2400000000000001 , 0.2500000000000001 , 
 0.2600000000000001 , 0.2700000000000001 , 0.2800000000000001 , 
 0.2900000000000001 , 0.3000000000000001 , 0.3100000000000001 , 
 0.3200000000000001 , 0.3300000000000001 , 0.3400000000000001 , 
 0.3500000000000001 , 0.3600000000000002 , 0.3700000000000002 , 
 0.3800000000000002 , 0.3900000000000002 , 0.4000000000000002 , 
 0.4100000000000002 , 0.4200000000000002 , 0.4300000000000002 , 
 0.4400000000000002 , 0.4500000000000002 , 0.4600000000000002 , 
 0.4700000000000003 , 0.4800000000000003 , 0.4900000000000003 , 
 0.5000000000000002 , 0.5100000000000002 , 0.5200000000000002 , 
 0.5300000000000002 , 0.5400000000000003 , 0.5500000000000003 , 
 0.5600000000000003 , 0.5700000000000003 , 0.5800000000000003 , 
 0.5900000000000003 , 0.6000000000000003 , 0.6100000000000003 , 
 0.6200000000000003 , 0.6300000000000003 , 0.6400000000000003 , 
 0.6500000000000004 , 0.6600000000000004 , 0.6700000000000004 , 
 0.6800000000000004 , 0.6900000000000004 , 0.7000000000000004 , 
 0.7100000000000004 , 0.7200000000000004 , 0.7300000000000004 , 
 0.7400000000000004 , 0.7500000000000004 , 0.7600000000000005 , 
 0.7700000000000005 , 0.7800000000000005 , 0.7900000000000005 , 
 0.8000000000000005 , 0.8100000000000005 , 0.8200000000000005 , 
 0.8300000000000005 , 0.8400000000000005 , 0.8500000000000005 , 
 0.8600000000000005 , 0.8700000000000006 , 0.8800000000000006 , 
 0.8900000000000006 , 0.9000000000000006 , 0.9100000000000006 , 
 0.9200000000000006 , 0.9300000000000006 , 0.9400000000000006 , 
 0.9500000000000006 , 0.9600000000000006 , 0.9700000000000006 , 
 0.9800000000000006 , 0.9900000000000007 \right] \right)=\left[ 1 , 
 1.014997750101248 , 1.029982003239722 , 1.044939274599006 , 
 1.05985610364446 , 1.0747190662368 , 1.089514786712912 , 
 1.10422994992305 , 1.118851313213567 , 1.133365718344415 , 
 1.14776010333067 , 1.162021514197434 , 1.176137116637545 , 
 1.190094207561581 , 1.203880226529785 , 1.217482767055615 , 
 1.230889587770742 , 1.244088623441454 , 1.257067995826556 , 
 1.269816024366985 , 1.282321236697518 , 1.294572378971135 , 
 1.306558425986717 , 1.318268591110984 , 1.329692335985737 , 
 1.340819380011667 , 1.351639709600205 , 1.362143587185071 , 
 1.37232155998543 , 1.382164468512753 , 1.391663454813742 , 
 1.400809970441889 , 1.409595784150499 , 1.41801298930026 , 
 1.426054010974682 , 1.433711612797009 , 1.440978903442474 , 
 1.447849342840024 , 1.454316748057942 , 1.460375298868068 , 
 1.466019542983613 , 1.471244400965849 , 1.476045170795258 , 
 1.480417532103036 , 1.484357550059133 , 1.48786167891333 , 
 1.49092676518618 , 1.493550050506925 , 1.495729174095843 , 
 1.49746217488879 , 1.498747493302027 , 1.499583972635738 , 
 1.499970860114983 , 1.499907807567145 , 1.499394871735262 , 
 1.498432514226959 , 1.497021601099038 , 1.495163402078079 , 
 1.492859589417777 , 1.490112236394023 , 1.486923815439098 , 
 1.483297195916649 , 1.479235641539457 , 1.474742807432315 , 
 1.469822736842662 , 1.464479857501934 , 1.458718977640905 , 
 1.4525452816626 , 1.44596432547669 , 1.438982031499539 , 
 1.431604683324436 , 1.423838920066784 , 1.415691730389341 , 
 1.407170446212898 , 1.398282736118043 , 1.38903659844396 , 
 1.379440354090461 , 1.369502639029735 , 1.359232396534563 , 
 1.348638869129968 , 1.337731590275575 , 1.326520375786132 , 
 1.315015314997945 , 1.303226761689157 , 1.29116532476204 , 
 1.278841858695708 , 1.26626745377781 , 1.253453426124026 , 
 1.240411307494323 , 1.227152834915152 , 1.213689940116914 , 
 1.200034738796209 , 1.186199519712527 , 1.172196733629194 , 
 1.158038982108526 , 1.143739006171271 , 1.129309674830555 , 
 1.114763973510631 , 1.100114992360884 , 1.085375914475572 \right] $$\>function fx(t) &= r(t)\*cos(t); $'fx(t)=fx(t)


$${\it fx}\left(\left[ 0 , 0.01 , 0.02 , 0.03 , 0.04 , 0.05 , 0.06 , 
 0.07 , 0.08 , 0.09 , 0.1 , 0.11 , 0.12 , 0.13 , 0.14 , 0.15 , 0.16
  , 0.17 , 0.18 , 0.19 , 0.2 , 0.21 , 0.2200000000000001 , 
 0.2300000000000001 , 0.2400000000000001 , 0.2500000000000001 , 
 0.2600000000000001 , 0.2700000000000001 , 0.2800000000000001 , 
 0.2900000000000001 , 0.3000000000000001 , 0.3100000000000001 , 
 0.3200000000000001 , 0.3300000000000001 , 0.3400000000000001 , 
 0.3500000000000001 , 0.3600000000000002 , 0.3700000000000002 , 
 0.3800000000000002 , 0.3900000000000002 , 0.4000000000000002 , 
 0.4100000000000002 , 0.4200000000000002 , 0.4300000000000002 , 
 0.4400000000000002 , 0.4500000000000002 , 0.4600000000000002 , 
 0.4700000000000003 , 0.4800000000000003 , 0.4900000000000003 , 
 0.5000000000000002 , 0.5100000000000002 , 0.5200000000000002 , 
 0.5300000000000002 , 0.5400000000000003 , 0.5500000000000003 , 
 0.5600000000000003 , 0.5700000000000003 , 0.5800000000000003 , 
 0.5900000000000003 , 0.6000000000000003 , 0.6100000000000003 , 
 0.6200000000000003 , 0.6300000000000003 , 0.6400000000000003 , 
 0.6500000000000004 , 0.6600000000000004 , 0.6700000000000004 , 
 0.6800000000000004 , 0.6900000000000004 , 0.7000000000000004 , 
 0.7100000000000004 , 0.7200000000000004 , 0.7300000000000004 , 
 0.7400000000000004 , 0.7500000000000004 , 0.7600000000000005 , 
 0.7700000000000005 , 0.7800000000000005 , 0.7900000000000005 , 
 0.8000000000000005 , 0.8100000000000005 , 0.8200000000000005 , 
 0.8300000000000005 , 0.8400000000000005 , 0.8500000000000005 , 
 0.8600000000000005 , 0.8700000000000006 , 0.8800000000000006 , 
 0.8900000000000006 , 0.9000000000000006 , 0.9100000000000006 , 
 0.9200000000000006 , 0.9300000000000006 , 0.9400000000000006 , 
 0.9500000000000006 , 0.9600000000000006 , 0.9700000000000006 , 
 0.9800000000000006 , 0.9900000000000007 \right] \right)=\left[ 1 , 
 1.014947000636657 , 1.029776013705529 , 1.044469087191079 , 
 1.059008331806833 , 1.073375947255439 , 1.087554248364218 , 
 1.101525691055367 , 1.11527289811021 , 1.128778684687222 , 
 1.142026083553954 , 1.154998369993414 , 1.16767908634602 , 
 1.180052066148761 , 1.192101457833886 , 1.203811747950136 , 
 1.215167783870255 , 1.226154795949382 , 1.236758419099762 , 
 1.246964713748154 , 1.256760186143285 , 1.266131807981756 , 
 1.275067035321848 , 1.283553826755846 , 1.29158066081265 , 
 1.29913655256367 , 1.306211069406282 , 1.312794346000405 , 
 1.318877098335118 , 1.324450636903608 , 1.329506878966172 , 
 1.334038359882425 , 1.338038243495345 , 1.341500331551311 , 
 1.344419072141793 , 1.346789567153917 , 1.348607578718725 , 
 1.349869534647481 , 1.350572532848044 , 1.350714344714907 , 
 1.350293417488142 , 1.349308875578123 , 1.347760520854542 , 
 1.345648831899879 , 1.342974962229111 , 1.339740737479097 , 
 1.335948651572729 , 1.331601861864506 , 1.326704183275865 , 
 1.321260081430156 , 1.315274664798767 , 1.308753675871437 , 
 1.301703481365363 , 1.294131061489226 , 1.286043998279732 , 
 1.277450463029762 , 1.268359202828647 , 1.25877952623647 , 
 1.248721288115691 , 1.238194873644713 , 1.227211181539273 , 
 1.215781606508839 , 1.203918020976346 , 1.191632756090801 , 
 1.17893858206338 , 1.165848687858719 , 1.152376660274093 , 
 1.138536462440146 , 1.124342411777761 , 1.10980915744646 , 
 1.094951657320579 , 1.079785154530145 , 1.064325153604093 , 
 1.04858739625406 , 1.032587836837555 , 1.0163426175398 , 
 0.999868043313951 , 0.9831805566197906 , 0.9662967120012925 , 
 0.9492331505436565 , 0.932006574250646 , 0.9146337203831 , 
 0.897131335799599 , 0.8795161513401855 , 0.8618048562939812 , 
 0.8440140729913906 , 0.8261603315613344 , 0.8082600448937051 , 
 0.7903294838468643 , 0.7723847527396025 , 0.754441765166499 , 
 0.7365162201750889 , 0.7186235788426429 , 0.7007790412897039 , 
 0.6829975241668103 , 0.6652936386500562 , 0.6476816689803099 , 
 0.6301755515800127 , 0.6127888547805567 , 0.595534759192214 \right] $$\>function fy(t) &= r(t)\*sin(t); $'fy(t)=fy(t)


$${\it fy}\left(\left[ 0 , 0.01 , 0.02 , 0.03 , 0.04 , 0.05 , 0.06 , 
 0.07 , 0.08 , 0.09 , 0.1 , 0.11 , 0.12 , 0.13 , 0.14 , 0.15 , 0.16
  , 0.17 , 0.18 , 0.19 , 0.2 , 0.21 , 0.2200000000000001 , 
 0.2300000000000001 , 0.2400000000000001 , 0.2500000000000001 , 
 0.2600000000000001 , 0.2700000000000001 , 0.2800000000000001 , 
 0.2900000000000001 , 0.3000000000000001 , 0.3100000000000001 , 
 0.3200000000000001 , 0.3300000000000001 , 0.3400000000000001 , 
 0.3500000000000001 , 0.3600000000000002 , 0.3700000000000002 , 
 0.3800000000000002 , 0.3900000000000002 , 0.4000000000000002 , 
 0.4100000000000002 , 0.4200000000000002 , 0.4300000000000002 , 
 0.4400000000000002 , 0.4500000000000002 , 0.4600000000000002 , 
 0.4700000000000003 , 0.4800000000000003 , 0.4900000000000003 , 
 0.5000000000000002 , 0.5100000000000002 , 0.5200000000000002 , 
 0.5300000000000002 , 0.5400000000000003 , 0.5500000000000003 , 
 0.5600000000000003 , 0.5700000000000003 , 0.5800000000000003 , 
 0.5900000000000003 , 0.6000000000000003 , 0.6100000000000003 , 
 0.6200000000000003 , 0.6300000000000003 , 0.6400000000000003 , 
 0.6500000000000004 , 0.6600000000000004 , 0.6700000000000004 , 
 0.6800000000000004 , 0.6900000000000004 , 0.7000000000000004 , 
 0.7100000000000004 , 0.7200000000000004 , 0.7300000000000004 , 
 0.7400000000000004 , 0.7500000000000004 , 0.7600000000000005 , 
 0.7700000000000005 , 0.7800000000000005 , 0.7900000000000005 , 
 0.8000000000000005 , 0.8100000000000005 , 0.8200000000000005 , 
 0.8300000000000005 , 0.8400000000000005 , 0.8500000000000005 , 
 0.8600000000000005 , 0.8700000000000006 , 0.8800000000000006 , 
 0.8900000000000006 , 0.9000000000000006 , 0.9100000000000006 , 
 0.9200000000000006 , 0.9300000000000006 , 0.9400000000000006 , 
 0.9500000000000006 , 0.9600000000000006 , 0.9700000000000006 , 
 0.9800000000000006 , 0.9900000000000007 \right] \right)=\left[ 0 , 
 0.01014980833556662 , 0.02059826678292271 , 0.03134347622283015 , 
 0.04238293991838228 , 0.05371356612987439 , 0.06533167172990376 , 
 0.07723298681299934 , 0.08941266029246918 , 0.1018652664755576 , 
 0.1145848126064173 , 0.1275647473648353 , 0.1407979703071057 , 
 0.1542768422339107 , 0.1679931964685752 , 0.1819383510275811 , 
 0.1961031216637831 , 0.2104778357613507 , 0.2250523470600841 , 
 0.2398160511854019 , 0.2547579019589912 , 0.2698664284638497 , 
 0.2851297528362152 , 0.3005356087557041 , 0.3160713606038417 , 
 0.3317240232600813 , 0.3474802825033731 , 0.3633265159863522 , 
 0.3792488147482899 , 0.3952330052320643 , 0.411264671769591 , 
 0.4273291794993832 , 0.4434116976792021 , 0.4594972233561165 , 
 0.4755706053556919 , 0.4916165685515136 , 0.5076197383757777 , 
 0.5235646655312819 , 0.5394358508648145 , 0.5552177703616642 , 
 0.5708949002207642 , 0.5864517419698421 , 0.6018728475798654 , 
 0.6171428445380648 , 0.6322464608388652 , 0.6471685498521687 , 
 0.6618941150286309 , 0.6764083344018014 , 0.6906965848473219 , 
 0.704744466059751 , 0.7185378242080237 , 0.7320627752310482 , 
 0.7453057277355214 , 0.7582534054586558 , 0.7708928692592016 , 
 0.7832115386008901 , 0.7951972124932317 , 0.8068380898554457 , 
 0.8181227892702304 , 0.8290403680950348 , 0.8395803408995157 , 
 0.8497326971989371 , 0.8594879184543822 , 0.8688369943118147 , 
 0.877771438053233 , 0.8862833012344233 , 0.894365187485098 , 
 0.9020102654485477 , 0.9092122808393135 , 0.91596556759876 , 
 0.9222650581299157 , 0.9281062925943645 , 0.9334854272555032 , 
 0.9383992418539865 , 0.9428451460027243 , 0.9468211845903713 , 
 0.9503260421838114 , 0.9533590464217597 , 0.9559201703932094 , 
 0.9580100339960551 , 0.9596299042728891 , 0.9607816947225576 , 
 0.9614679635877484 , 0.9616919111204768 , 0.9614573758289937 , 
 0.9607688297112769 , 0.9596313724818526 , 0.9580507248003547 , 
 0.9560332205117796 , 0.9535857979100135 , 0.950715990037748 , 
 0.9474319140374602 , 0.9437422595696462 , 0.9396562763159917 , 
 0.9351837605866338 , 0.9303350410521015 , 0.9251209636219332 , 
 0.9195528754933222 , 0.9136426083945087 , 0.9074024610488752
  \right] $$\>function ds(t) &= trigreduce(radcan(sqrt(diff(fx(t),t)^2+diff(fy(t),t)^2))); $'ds(t)=ds(t)


    Maxima said:
    diff: second argument must be a variable; found errexp1
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    ... e(radcan(sqrt(diff(fx(t),t)^2+diff(fy(t),t)^2))); $'ds(t)=ds(t ...
                                                         ^

\>$integrate(ds(x),x,0,2\*pi) //panjang (keliling) kurva


$$\int_{0}^{2\,\pi}{{\it ds}\left(x\right)\;dx}$$Maxima gagal melakukan perhitungan eksak integral tersebut.


Berikut kita hitung integralnya secara umerik dengan perintah EMT.


\>integrate("ds(x)",0,2\*pi)


    Function ds not found.
    Try list ... to find functions!
    Error in expression: ds(x)
    %mapexpression1:
        return expr(x,args());
    Error in map.
    %evalexpression:
        if maps then return %mapexpression1(x,f$;args());
    gauss:
        if maps then y=%evalexpression(f$,a+h-(h*xn)',maps;args());
    adaptivegauss:
        t1=gauss(f$,c,c+h;args(),=maps);
    Try "trace errors" to inspect local variables after errors.
    integrate:
        return adaptivegauss(f$,a,b,eps*1000;args(),=maps);

Spiral Logaritmik


$$x=e^{ax}\cos x,\ y=e^{ax}\sin x.$$\>a=0.1; plot2d("exp(a\*x)\*cos(x)","exp(a\*x)\*sin(x)",r=2,xmin=0,xmax=2\*pi):


![images/EMT4Kalkulus%20(1)-229.png](images/EMT4Kalkulus%20(1)-229.png)

\>&kill(a) // hapus expresi a


    
                                     done
    

\>function fx(t) &= exp(a\*t)\*cos(t); $'fx(t)=fx(t)


$${\it fx}\left(\left[ 0 , 0.01 , 0.02 , 0.03 , 0.04 , 0.05 , 0.06 , 
 0.07 , 0.08 , 0.09 , 0.1 , 0.11 , 0.12 , 0.13 , 0.14 , 0.15 , 0.16
  , 0.17 , 0.18 , 0.19 , 0.2 , 0.21 , 0.2200000000000001 , 
 0.2300000000000001 , 0.2400000000000001 , 0.2500000000000001 , 
 0.2600000000000001 , 0.2700000000000001 , 0.2800000000000001 , 
 0.2900000000000001 , 0.3000000000000001 , 0.3100000000000001 , 
 0.3200000000000001 , 0.3300000000000001 , 0.3400000000000001 , 
 0.3500000000000001 , 0.3600000000000002 , 0.3700000000000002 , 
 0.3800000000000002 , 0.3900000000000002 , 0.4000000000000002 , 
 0.4100000000000002 , 0.4200000000000002 , 0.4300000000000002 , 
 0.4400000000000002 , 0.4500000000000002 , 0.4600000000000002 , 
 0.4700000000000003 , 0.4800000000000003 , 0.4900000000000003 , 
 0.5000000000000002 , 0.5100000000000002 , 0.5200000000000002 , 
 0.5300000000000002 , 0.5400000000000003 , 0.5500000000000003 , 
 0.5600000000000003 , 0.5700000000000003 , 0.5800000000000003 , 
 0.5900000000000003 , 0.6000000000000003 , 0.6100000000000003 , 
 0.6200000000000003 , 0.6300000000000003 , 0.6400000000000003 , 
 0.6500000000000004 , 0.6600000000000004 , 0.6700000000000004 , 
 0.6800000000000004 , 0.6900000000000004 , 0.7000000000000004 , 
 0.7100000000000004 , 0.7200000000000004 , 0.7300000000000004 , 
 0.7400000000000004 , 0.7500000000000004 , 0.7600000000000005 , 
 0.7700000000000005 , 0.7800000000000005 , 0.7900000000000005 , 
 0.8000000000000005 , 0.8100000000000005 , 0.8200000000000005 , 
 0.8300000000000005 , 0.8400000000000005 , 0.8500000000000005 , 
 0.8600000000000005 , 0.8700000000000006 , 0.8800000000000006 , 
 0.8900000000000006 , 0.9000000000000006 , 0.9100000000000006 , 
 0.9200000000000006 , 0.9300000000000006 , 0.9400000000000006 , 
 0.9500000000000006 , 0.9600000000000006 , 0.9700000000000006 , 
 0.9800000000000006 , 0.9900000000000007 \right] \right)=\left[ 1 , 
 0.9999500004166653\,e^{0.01\,a} , 0.9998000066665778\,e^{0.02\,a} , 
 0.9995500337489875\,e^{0.03\,a} , 0.9992001066609779\,e^{0.04\,a} , 
 0.9987502603949663\,e^{0.05\,a} , 0.9982005399352042\,e^{0.06\,a} , 
 0.9975510002532796\,e^{0.07\,a} , 0.9968017063026194\,e^{0.08\,a} , 
 0.9959527330119943\,e^{0.09\,a} , 0.9950041652780258\,e^{0.1\,a} , 
 0.9939560979566968\,e^{0.11\,a} , 0.9928086358538663\,e^{0.12\,a} , 
 0.9915618937147881\,e^{0.13\,a} , 0.9902159962126372\,e^{0.14\,a} , 
 0.9887710779360422\,e^{0.15\,a} , 0.9872272833756269\,e^{0.16\,a} , 
 0.9855847669095608\,e^{0.17\,a} , 0.9838436927881214\,e^{0.18\,a} , 
 0.9820042351172703\,e^{0.19\,a} , 0.9800665778412416\,e^{0.2\,a} , 
 0.9780309147241483\,e^{0.21\,a} , 0.9758974493306055\,e^{
 0.2200000000000001\,a} , 0.9736663950053748\,e^{0.2300000000000001\,
 a} , 0.9713379748520296\,e^{0.2400000000000001\,a} , 
 0.9689124217106447\,e^{0.2500000000000001\,a} , 0.9663899781345132\,
 e^{0.2600000000000001\,a} , 0.9637708963658905\,e^{
 0.2700000000000001\,a} , 0.9610554383107709\,e^{0.2800000000000001\,
 a} , 0.9582438755126972\,e^{0.2900000000000001\,a} , 
 0.955336489125606\,e^{0.3000000000000001\,a} , 0.9523335698857134\,e
 ^{0.3100000000000001\,a} , 0.9492354180824408\,e^{0.3200000000000001
 \,a} , 0.9460423435283869\,e^{0.3300000000000001\,a} , 
 0.9427546655283462\,e^{0.3400000000000001\,a} , 0.9393727128473789\,
 e^{0.3500000000000001\,a} , 0.9358968236779348\,e^{
 0.3600000000000002\,a} , 0.9323273456060344\,e^{0.3700000000000002\,
 a} , 0.9286646355765101\,e^{0.3800000000000002\,a} , 
 0.924909059857313\,e^{0.3900000000000002\,a} , 0.921060994002885\,e
 ^{0.4000000000000002\,a} , 0.917120822816605\,e^{0.4100000000000002
 \,a} , 0.9130889403123081\,e^{0.4200000000000002\,a} , 
 0.9089657496748851\,e^{0.4300000000000002\,a} , 0.9047516632199634\,
 e^{0.4400000000000002\,a} , 0.9004471023526768\,e^{
 0.4500000000000002\,a} , 0.8960524975255252\,e^{0.4600000000000002\,
 a} , 0.8915682881953289\,e^{0.4700000000000003\,a} , 
 0.886994922779284\,e^{0.4800000000000003\,a} , 0.8823328586101213\,e
 ^{0.4900000000000003\,a} , 0.8775825618903726\,e^{0.5000000000000002
 \,a} , 0.8727445076457512\,e^{0.5100000000000002\,a} , 
 0.8678191796776498\,e^{0.5200000000000002\,a} , 0.8628070705147609\,
 e^{0.5300000000000002\,a} , 0.857708681363824\,e^{0.5400000000000003
 \,a} , 0.8525245220595056\,e^{0.5500000000000003\,a} , 
 0.847255111013416\,e^{0.5600000000000003\,a} , 0.8419009751622686\,e
 ^{0.5700000000000003\,a} , 0.8364626499151868\,e^{0.5800000000000003
 \,a} , 0.8309406791001633\,e^{0.5900000000000003\,a} , 
 0.8253356149096781\,e^{0.6000000000000003\,a} , 0.8196480178454794\,
 e^{0.6100000000000003\,a} , 0.8138784566625338\,e^{
 0.6200000000000003\,a} , 0.8080275083121516\,e^{0.6300000000000003\,
 a} , 0.8020957578842924\,e^{0.6400000000000003\,a} , 
 0.7960837985490556\,e^{0.6500000000000004\,a} , 0.7899922314973649\,
 e^{0.6600000000000004\,a} , 0.783821665880849\,e^{0.6700000000000004
 \,a} , 0.7775727187509277\,e^{0.6800000000000004\,a} , 
 0.7712460149971063\,e^{0.6900000000000004\,a} , 0.7648421872844882\,
 e^{0.7000000000000004\,a} , 0.7583618759905079\,e^{
 0.7100000000000004\,a} , 0.7518057291408947\,e^{0.7200000000000004\,
 a} , 0.7451744023448701\,e^{0.7300000000000004\,a} , 
 0.7384685587295876\,e^{0.7400000000000004\,a} , 0.7316888688738206\,
 e^{0.7500000000000004\,a} , 0.7248360107409049\,e^{
 0.7600000000000005\,a} , 0.7179106696109431\,e^{0.7700000000000005\,
 a} , 0.7109135380122771\,e^{0.7800000000000005\,a} , 
 0.7038453156522357\,e^{0.7900000000000005\,a} , 0.696706709347165\,e
 ^{0.8000000000000005\,a} , 0.6894984329517466\,e^{0.8100000000000005
 \,a} , 0.6822212072876132\,e^{0.8200000000000005\,a} , 
 0.6748757600712667\,e^{0.8300000000000005\,a} , 0.6674628258413078\,
 e^{0.8400000000000005\,a} , 0.6599831458849817\,e^{
 0.8500000000000005\,a} , 0.6524374681640515\,e^{0.8600000000000005\,
 a} , 0.6448265472400008\,e^{0.8700000000000006\,a} , 
 0.6371511441985798\,e^{0.8800000000000006\,a} , 0.6294120265736964\,
 e^{0.8900000000000006\,a} , 0.6216099682706641\,e^{
 0.9000000000000006\,a} , 0.6137457494888111\,e^{0.9100000000000006\,
 a} , 0.6058201566434623\,e^{0.9200000000000006\,a} , 
 0.5978339822872978\,e^{0.9300000000000006\,a} , 0.5897880250310977\,
 e^{0.9400000000000006\,a} , 0.581683089463883\,e^{0.9500000000000006
 \,a} , 0.5735199860724561\,e^{0.9600000000000006\,a} , 
 0.5652995311603538\,e^{0.9700000000000006\,a} , 0.5570225467662168\,
 e^{0.9800000000000006\,a} , 0.548689860581587\,e^{0.9900000000000007
 \,a} \right] $$\>function fy(t) &= exp(a\*t)\*sin(t); $'fy(t)=fy(t)


$${\it fy}\left(\left[ 0 , 0.01 , 0.02 , 0.03 , 0.04 , 0.05 , 0.06 , 
 0.07 , 0.08 , 0.09 , 0.1 , 0.11 , 0.12 , 0.13 , 0.14 , 0.15 , 0.16
  , 0.17 , 0.18 , 0.19 , 0.2 , 0.21 , 0.2200000000000001 , 
 0.2300000000000001 , 0.2400000000000001 , 0.2500000000000001 , 
 0.2600000000000001 , 0.2700000000000001 , 0.2800000000000001 , 
 0.2900000000000001 , 0.3000000000000001 , 0.3100000000000001 , 
 0.3200000000000001 , 0.3300000000000001 , 0.3400000000000001 , 
 0.3500000000000001 , 0.3600000000000002 , 0.3700000000000002 , 
 0.3800000000000002 , 0.3900000000000002 , 0.4000000000000002 , 
 0.4100000000000002 , 0.4200000000000002 , 0.4300000000000002 , 
 0.4400000000000002 , 0.4500000000000002 , 0.4600000000000002 , 
 0.4700000000000003 , 0.4800000000000003 , 0.4900000000000003 , 
 0.5000000000000002 , 0.5100000000000002 , 0.5200000000000002 , 
 0.5300000000000002 , 0.5400000000000003 , 0.5500000000000003 , 
 0.5600000000000003 , 0.5700000000000003 , 0.5800000000000003 , 
 0.5900000000000003 , 0.6000000000000003 , 0.6100000000000003 , 
 0.6200000000000003 , 0.6300000000000003 , 0.6400000000000003 , 
 0.6500000000000004 , 0.6600000000000004 , 0.6700000000000004 , 
 0.6800000000000004 , 0.6900000000000004 , 0.7000000000000004 , 
 0.7100000000000004 , 0.7200000000000004 , 0.7300000000000004 , 
 0.7400000000000004 , 0.7500000000000004 , 0.7600000000000005 , 
 0.7700000000000005 , 0.7800000000000005 , 0.7900000000000005 , 
 0.8000000000000005 , 0.8100000000000005 , 0.8200000000000005 , 
 0.8300000000000005 , 0.8400000000000005 , 0.8500000000000005 , 
 0.8600000000000005 , 0.8700000000000006 , 0.8800000000000006 , 
 0.8900000000000006 , 0.9000000000000006 , 0.9100000000000006 , 
 0.9200000000000006 , 0.9300000000000006 , 0.9400000000000006 , 
 0.9500000000000006 , 0.9600000000000006 , 0.9700000000000006 , 
 0.9800000000000006 , 0.9900000000000007 \right] \right)=\left[ 0 , 
 0.009999833334166664\,e^{0.01\,a} , 0.01999866669333308\,e^{0.02\,a}
  , 0.02999550020249566\,e^{0.03\,a} , 0.03998933418663416\,e^{0.04\,
 a} , 0.04997916927067833\,e^{0.05\,a} , 0.0599640064794446\,e^{0.06
 \,a} , 0.06994284733753277\,e^{0.07\,a} , 0.0799146939691727\,e^{
 0.08\,a} , 0.08987854919801104\,e^{0.09\,a} , 0.09983341664682814\,e
 ^{0.1\,a} , 0.1097783008371748\,e^{0.11\,a} , 0.1197122072889193\,e
 ^{0.12\,a} , 0.1296341426196948\,e^{0.13\,a} , 0.1395431146442365\,e
 ^{0.14\,a} , 0.1494381324735992\,e^{0.15\,a} , 0.159318206614246\,e
 ^{0.16\,a} , 0.169182349066996\,e^{0.17\,a} , 0.1790295734258242\,e
 ^{0.18\,a} , 0.1888588949765006\,e^{0.19\,a} , 0.1986693307950612\,e
 ^{0.2\,a} , 0.2084598998460996\,e^{0.21\,a} , 0.2182296230808694\,e
 ^{0.2200000000000001\,a} , 0.2279775235351885\,e^{0.2300000000000001
 \,a} , 0.2377026264271347\,e^{0.2400000000000001\,a} , 
 0.247403959254523\,e^{0.2500000000000001\,a} , 0.2570805518921552\,e
 ^{0.2600000000000001\,a} , 0.2667314366888312\,e^{0.2700000000000001
 \,a} , 0.2763556485641138\,e^{0.2800000000000001\,a} , 
 0.2859522251048356\,e^{0.2900000000000001\,a} , 0.2955202066613397\,
 e^{0.3000000000000001\,a} , 0.3050586364434436\,e^{
 0.3100000000000001\,a} , 0.3145665606161179\,e^{0.3200000000000001\,
 a} , 0.3240430283948685\,e^{0.3300000000000001\,a} , 
 0.3334870921408145\,e^{0.3400000000000001\,a} , 0.3428978074554515\,
 e^{0.3500000000000001\,a} , 0.3522742332750901\,e^{
 0.3600000000000002\,a} , 0.3616154319649622\,e^{0.3700000000000002\,
 a} , 0.3709204694129828\,e^{0.3800000000000002\,a} , 
 0.3801884151231616\,e^{0.3900000000000002\,a} , 0.3894183423086507\,
 e^{0.4000000000000002\,a} , 0.3986093279844231\,e^{
 0.4100000000000002\,a} , 0.4077604530595704\,e^{0.4200000000000002\,
 a} , 0.416870802429211\,e^{0.4300000000000002\,a} , 
 0.4259394650659998\,e^{0.4400000000000002\,a} , 0.4349655341112304\,
 e^{0.4500000000000002\,a} , 0.44394810696552\,e^{0.4600000000000002
 \,a} , 0.4528862853790685\,e^{0.4700000000000003\,a} , 
 0.4617791755414831\,e^{0.4800000000000003\,a} , 0.4706258881711582\,
 e^{0.4900000000000003\,a} , 0.4794255386042032\,e^{
 0.5000000000000002\,a} , 0.4881772468829077\,e^{0.5100000000000002\,
 a} , 0.4968801378437369\,e^{0.5200000000000002\,a} , 
 0.5055333412048472\,e^{0.5300000000000002\,a} , 0.5141359916531133\,
 e^{0.5400000000000003\,a} , 0.5226872289306594\,e^{
 0.5500000000000003\,a} , 0.5311861979208836\,e^{0.5600000000000003\,
 a} , 0.5396320487339695\,e^{0.5700000000000003\,a} , 
 0.5480239367918738\,e^{0.5800000000000003\,a} , 0.556361022912784\,e
 ^{0.5900000000000003\,a} , 0.5646424733950356\,e^{0.6000000000000003
 \,a} , 0.5728674601004815\,e^{0.6100000000000003\,a} , 
 0.5810351605373053\,e^{0.6200000000000003\,a} , 0.5891447579422698\,
 e^{0.6300000000000003\,a} , 0.5971954413623923\,e^{
 0.6400000000000003\,a} , 0.6051864057360399\,e^{0.6500000000000004\,
 a} , 0.6131168519734341\,e^{0.6600000000000004\,a} , 
 0.6209859870365599\,e^{0.6700000000000004\,a} , 0.6287930240184688\,
 e^{0.6800000000000004\,a} , 0.6365371822219682\,e^{
 0.6900000000000004\,a} , 0.6442176872376913\,e^{0.7000000000000004\,
 a} , 0.651833771021537\,e^{0.7100000000000004\,a} , 
 0.6593846719714734\,e^{0.7200000000000004\,a} , 0.6668696350036982\,
 e^{0.7300000000000004\,a} , 0.6742879116281454\,e^{
 0.7400000000000004\,a} , 0.6816387600233345\,e^{0.7500000000000004\,
 a} , 0.6889214451105516\,e^{0.7600000000000005\,a} , 
 0.696135238627357\,e^{0.7700000000000005\,a} , 0.7032794192004105\,e
 ^{0.7800000000000005\,a} , 0.7103532724176082\,e^{0.7900000000000005
 \,a} , 0.7173560908995231\,e^{0.8000000000000005\,a} , 
 0.7242871743701429\,e^{0.8100000000000005\,a} , 0.7311458297268962\,
 e^{0.8200000000000005\,a} , 0.7379313711099631\,e^{
 0.8300000000000005\,a} , 0.7446431199708596\,e^{0.8400000000000005\,
 a} , 0.751280405140293\,e^{0.8500000000000005\,a} , 
 0.7578425628952773\,e^{0.8600000000000005\,a} , 0.7643289370255054\,
 e^{0.8700000000000006\,a} , 0.7707388788989696\,e^{
 0.8800000000000006\,a} , 0.7770717475268242\,e^{0.8900000000000006\,
 a} , 0.7833269096274837\,e^{0.9000000000000006\,a} , 
 0.7895037396899508\,e^{0.9100000000000006\,a} , 0.7956016200363664\,
 e^{0.9200000000000006\,a} , 0.8016199408837775\,e^{
 0.9300000000000006\,a} , 0.8075581004051147\,e^{0.9400000000000006\,
 a} , 0.8134155047893741\,e^{0.9500000000000006\,a} , 
 0.8191915683009986\,e^{0.9600000000000006\,a} , 0.8248857133384504\,
 e^{0.9700000000000006\,a} , 0.8304973704919708\,e^{
 0.9800000000000006\,a} , 0.8360259786005209\,e^{0.9900000000000007\,
 a} \right] $$\>function df(t) &= trigreduce(radcan(sqrt(diff(fx(t),t)^2+diff(fy(t),t)^2))); $'df(t)=df(t)


    Maxima said:
    diff: second argument must be a variable; found errexp1
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    ... e(radcan(sqrt(diff(fx(t),t)^2+diff(fy(t),t)^2))); $'df(t)=df(t ...
                                                         ^

\>S &=integrate(df(t),t,0,2\*%pi); $S // panjang kurva (spiral)


    Maxima said:
    defint: variable of integration cannot be a constant; found errexp1
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    S &amp;=integrate(df(t),t,0,2*%pi); $S // panjang kurva (spiral) ...
                                  ^

\>S(a=0.1) // Panjang kurva untuk a=0.1


    Function S not found.
    Try list ... to find functions!
    Error in:
    S(a=0.1) // Panjang kurva untuk a=0.1 ...
            ^

Soal:


Tunjukkan bahwa keliling lingkaran dengan jari-jari r adalah K=2.pi.r.


Berikut adalah contoh menghitung panjang parabola.


\>plot2d("x^2",xmin=-1,xmax=1):


![images/EMT4Kalkulus%20(1)-232.png](images/EMT4Kalkulus%20(1)-232.png)

\>$showev('integrate(sqrt(1+diff(x^2,x)^2),x,-1,1))


$$\int_{-1}^{1}{\sqrt{4\,x^2+1}\;dx}=\frac{{\rm asinh}\; 2+2\,\sqrt{5
 }}{2}$$\>$float(%)


$$\int_{-1.0}^{1.0}{\sqrt{4.0\,x^2+1.0}\;dx}=2.957885715089195$$\>x=-1:0.2:1; y=x^2; plot2d(x,y);  ...  
\>     plot2d(x,y,points=1,style="o#",add=1):


![images/EMT4Kalkulus%20(1)-235.png](images/EMT4Kalkulus%20(1)-235.png)

Panjang tersebut dapat dihampiri dengan menggunakan jumlah panjang ruas-ruas garis yang menghubungkan titik-titik pada parabola
tersebut.


\>i=1:cols(x)-1; sum(sqrt((x[i+1]-x[i])^2+(y[i+1]-y[i])^2))


    2.95191957027

Hasilnya mendekati panjang yang dihitung secara eksak. Untuk
mendapatkan hampiran yang cukup akurat, jarak antar titik dapat
diperkecil, misalnya 0.1, 0.05, 0.01, dan seterusnya. Cobalah Anda
ulangi perhitungannya dengan nilai-nilai tersebut.


## Koordinat Kartesius

Berikut diberikan contoh perhitungan panjang kurva menggunakan
koordinat Kartesius. Kita akan hitung panjang kurva dengan persamaan
implisit:


$$x^3+y^3-3xy=0.$$\>z &= x^3+y^3-3\*x\*y; $z


$$y^3-3\,x\,y+x^3$$\>plot2d(z,r=2,level=0,n=100):


![images/EMT4Kalkulus%20(1)-238.png](images/EMT4Kalkulus%20(1)-238.png)

Kita tertarik pada kurva di kuadran pertama.


\>plot2d(z,a=0,b=2,c=0,d=2,level=[-10;0],n=100,contourwidth=3,style="/"):


![images/EMT4Kalkulus%20(1)-239.png](images/EMT4Kalkulus%20(1)-239.png)

Kita selesaikan persamaannya untuk x.


\>$z with y=l\*x, sol &= solve(%,x); $sol


$$l^3\,x^3+x^3-3\,l\,x^2$$$$\left[ x=\frac{3\,l}{l^3+1} , x=0 \right] $$Kita gunakan solusi tersebut untuk mendefinisikan fungsi dengan Maxima.


\>function f(l) &= rhs(sol[1]); $'f(l)=f(l)


$$f\left(l\right)=\frac{3\,l}{l^3+1}$$Fungsi tersebut juga dapat digunaka untuk menggambar kurvanya. Ingat, bahwa fungsi tersebut adalah nilai x dan nilai y=l*x, yakni
x=f(l) dan y=l*f(l).


\>plot2d(&f(x),&x\*f(x),xmin=-0.5,xmax=2,a=0,b=2,c=0,d=2,r=1.5):


![images/EMT4Kalkulus%20(1)-243.png](images/EMT4Kalkulus%20(1)-243.png)

Elemen panjang kurva adalah:


$$ds=\sqrt{f'(l)^2+(lf'(l)+f(l))^2}.$$\>function ds(l) &= ratsimp(sqrt(diff(f(l),l)^2+diff(l\*f(l),l)^2)); $'ds(l)=ds(l)


$${\it ds}\left(l\right)=\frac{\sqrt{9\,l^8+36\,l^6-36\,l^5-36\,l^3+
 36\,l^2+9}}{\sqrt{l^{12}+4\,l^9+6\,l^6+4\,l^3+1}}$$\>$integrate(ds(l),l,0,1)


$$\int_{0}^{1}{\frac{\sqrt{9\,l^8+36\,l^6-36\,l^5-36\,l^3+36\,l^2+9}
 }{\sqrt{l^{12}+4\,l^9+6\,l^6+4\,l^3+1}}\;dl}$$Integral tersebut tidak dapat dihitung secara eksak menggunakan Maxima. Kita hitung integral etrsebut secara numerik dengan Euler.
Karena kurva simetris, kita hitung untuk nilai variabel integrasi dari 0 sampai 1, kemudian hasilnya dikalikan 2. 


\>2\*integrate("ds(x)",0,1)


    4.91748872168

\>2\*romberg(&ds(x),0,1)// perintah Euler lain untuk menghitung nilai hampiran integral yang sama


    4.91748872168

Perhitungan di datas dapat dilakukan untuk sebarang fungsi x dan y dengan mendefinisikan fungsi EMT, misalnya kita beri nama
panjangkurva. Fungsi ini selalu memanggil Maxima untuk menurunkan fungsi yang diberikan.


\>function panjangkurva(fx,fy,a,b) ...


    ds=mxm("sqrt(diff(@fx,x)^2+diff(@fy,x)^2)");
    return romberg(ds,a,b);
    endfunction
</pre>
\>panjangkurva("x","x^2",-1,1) // cek untuk menghitung panjang kurva parabola sebelumnya


    2.95788571509

Bandingkan dengan nilai eksak di atas.


\>2\*panjangkurva(mxm("f(x)"),mxm("x\*f(x)"),0,1) // cek contoh terakhir, bandingkan hasilnya!


    4.91748872168

Kita hitung panjang spiral Archimides berikut ini dengan fungsi tersebut.


\>plot2d("x\*cos(x)","x\*sin(x)",xmin=0,xmax=2\*pi,square=1):


![images/EMT4Kalkulus%20(1)-247.png](images/EMT4Kalkulus%20(1)-247.png)

\>panjangkurva("x\*cos(x)","x\*sin(x)",0,2\*pi)


    21.2562941482

Berikut kita definisikan fungsi yang sama namun dengan Maxima, untuk perhitungan eksak.


\>&kill(ds,x,fx,fy)


    
                                     done
    

\>function ds(fx,fy) &&= sqrt(diff(fx,x)^2+diff(fy,x)^2)


    
                               2              2
                      sqrt(diff (fy, x) + diff (fx, x))
    

\>sol &= ds(x\*cos(x),x\*sin(x)); $sol // Kita gunakan untuk menghitung panjang kurva terakhir di atas


$$\sqrt{\left(\cos x-x\,\sin x\right)^2+\left(\sin x+x\,\cos x\right)
 ^2}$$\>$sol | trigreduce | expand, $integrate(%,x,0,2\*pi), %()


$$\sqrt{x^2+1}$$$$\frac{{\rm asinh}\; \left(2\,\pi\right)+2\,\pi\,\sqrt{4\,\pi^2+1}}{
 2}$$    21.2562941482

Hasilnya sama dengan perhitungan menggunakan fungsi EMT.


Berikut adalah contoh lain penggunaan fungsi Maxima tersebut.


\>plot2d("3\*x^2-1","3\*x^3-1",xmin=-1/sqrt(3),xmax=1/sqrt(3),square=1):


![images/EMT4Kalkulus%20(1)-251.png](images/EMT4Kalkulus%20(1)-251.png)

\>sol &= radcan(ds(3\*x^2-1,3\*x^3-1)); $sol


$$3\,x\,\sqrt{9\,x^2+4}$$\>$showev('integrate(sol,x,0,1/sqrt(3))), $2\*float(%) // panjang kurva di atas


$$3\,\int_{0}^{\frac{1}{\sqrt{3}}}{x\,\sqrt{9\,x^2+4}\;dx}=3\,\left(
 \frac{7^{\frac{3}{2}}}{27}-\frac{8}{27}\right)$$$$6.0\,\int_{0.0}^{0.5773502691896258}{x\,\sqrt{9.0\,x^2+4.0}\;dx}=
 2.337835372767141$$## Sikloid

Berikut kita akan menghitung panjang kurva lintasan (sikloid) suatu
titik pada lingkaran yang berputar ke kanan pada permukaan datar.
Misalkan jari-jari lingkaran tersebut adalah r. Posisi titik pusat
lingkaran pada saat t adalah:


$$(rt,r).$$Misalkan posisi titik pada lingkaran tersebut mula-mula (0,0) dan
posisinya pada saat t adalah:


$$(r(t-\sin(t)),r(1-\cos(t))).$$Berikut kita plot lintasan tersebut dan beberapa posisi lingkaran
ketika t=0, t=pi/2, t=r*pi.


\>x &= r\*(t-sin(t))


    
            [0, 1.66665833335744e-7 r, 1.33330666692022e-6 r, 
    4.499797504338432e-6 r, 1.066581336583994e-5 r, 
    2.083072932167196e-5 r, 3.599352055540239e-5 r, 
    5.71526624672386e-5 r, 8.530603082730626e-5 r, 
    1.214508019889565e-4 r, 1.665833531718508e-4 r, 
    2.216991628251896e-4 r, 2.877927110806339e-4 r, 
    3.658573803051457e-4 r, 4.568853557635201e-4 r, 
    5.618675264007778e-4 r, 6.817933857540259e-4 r, 
    8.176509330039827e-4 r, 9.704265741758145e-4 r, 
    0.001141105023499428 r, 0.001330669204938795 r, 
    0.001540100153900437 r, 0.001770376919130678 r, 
    0.002022476464811601 r, 0.002297373572865413 r, 
    0.002596040745477063 r, 0.002919448107844891 r, 
    0.003268563311168871 r, 0.003644351435886262 r, 
    0.004047774895164447 r, 0.004479793338660443 r, 0.0049413635565565 r, 
    0.005433439383882244 r, 0.005956971605131645 r, 
    0.006512907859185624 r, 0.007102192544548636 r, 
    0.007725766724910044 r, 0.00838456803503801 r, 
    0.009079530587017326 r, 0.009811584876838586 r, 0.0105816576913495 r, 
    0.01139067201557714 r, 0.01223954694042984 r, 0.01312919757078923 r, 
    0.01406053493400045 r, 0.01503446588876983 r, 0.01605189303448024 r, 
    0.01711371462093175 r, 0.01822082445851714 r, 0.01937411182884202 r, 
    0.02057446139579705 r, 0.02182275311709253 r, 0.02311986215626333 r, 
    0.02446665879515308 r, 0.02586400834688696 r, 0.02731277106934082 r, 
    0.02881380207911666 r, 0.03036795126603076 r, 0.03197606320812652 r, 
    0.0336389770872163 r, 0.03535752660496472 r, 0.03713253989951881 r, 
    0.03896483946269502 r, 0.0408552420577305 r, 0.04280455863760801 r, 
    0.04481359426396048 r, 0.04688314802656623 r, 0.04901401296344043 r, 
    0.05120697598153157 r, 0.05346281777803219 r, 0.05578231276230905 r, 
    0.05816622897846346 r, 0.06061532802852698 r, 0.0631303649963022 r, 
    0.06571208837185505 r, 0.06836123997666599 r, 0.07107855488944881 r, 
    0.07386476137264342 r, 0.07672058079958999 r, 0.07964672758239233 r, 
    0.08264390910047736 r, 0.0857128256298576 r, 0.08885417027310427 r, 
    0.09206862889003742 r, 0.09535688002914089 r, 0.0987195948597075 r, 
    0.1021574371047232 r, 0.1056710629744951 r, 0.1092611211010309 r, 
    0.1129282524731764 r, 0.1166730903725168 r, 0.1204962603100498 r, 
    0.1243983799636342 r, 0.1283800591162231 r, 0.1324418995948859 r, 
    0.1365844952106265 r, 0.140808431699002 r, 0.1451142866615502 r, 
    0.1495026295080298 r, 0.1539740213994798 r]
    

\>y &= r\*(1-cos(t))


    
            [0, 4.999958333473664e-5 r, 1.999933334222437e-4 r, 
    4.499662510124569e-4 r, 7.998933390220841e-4 r, 
    0.001249739605033717 r, 0.00179946006479581 r, 
    0.002448999746720415 r, 0.003198293697380561 r, 
    0.004047266988005727 r, 0.004995834721974179 r, 
    0.006043902043303184 r, 0.00719136414613375 r, 0.00843810628521191 r, 
    0.009784003787362772 r, 0.01122892206395776 r, 0.01277271662437307 r, 
    0.01441523309043924 r, 0.01615630721187855 r, 0.01799576488272969 r, 
    0.01993342215875837 r, 0.02196908527585173 r, 0.02410255066939448 r, 
    0.02633360499462523 r, 0.02866202514797045 r, 0.03108757828935527 r, 
    0.03361002186548678 r, 0.03622910363410947 r, 0.03894456168922911 r, 
    0.04175612448730281 r, 0.04466351087439402 r, 0.04766643011428662 r, 
    0.05076458191755917 r, 0.0539576564716131 r, 0.05724533447165381 r, 
    0.06062728715262111 r, 0.06410317632206519 r, 0.06767265439396564 r, 
    0.07133536442348987 r, 0.07509094014268702 r, 0.07893900599711501 r, 
    0.08287917718339499 r, 0.08691105968769186 r, 0.09103425032511492 r, 
    0.09524833678003664 r, 0.09955289764732322 r, 0.1039475024744748 r, 
    0.1084317118046711 r, 0.113005077220716 r, 0.1176671413898787 r, 
    0.1224174381096274 r, 0.1272554923542488 r, 0.1321808203223502 r, 
    0.1371929294852391 r, 0.1422913186361759 r, 0.1474754779404944 r, 
    0.152744888986584 r, 0.1580990248377314 r, 0.1635373500848132 r, 
    0.1690593208998367 r, 0.1746643850903219 r, 0.1803519821545206 r, 
    0.1861215433374662 r, 0.1919724916878484 r, 0.1979042421157076 r, 
    0.2039162014509444 r, 0.2100077685026351 r, 0.216178334119151 r, 
    0.2224272812490723 r, 0.2287539850028937 r, 0.2351578127155118 r, 
    0.2416381240094921 r, 0.2481942708591053 r, 0.2548255976551299 r, 
    0.2615314412704124 r, 0.2683111311261794 r, 0.2751639892590951 r, 
    0.2820893303890569 r, 0.2890864619877229 r, 0.2961546843477643 r, 
    0.3032932906528349 r, 0.3105015670482534 r, 0.3177787927123868 r, 
    0.3251242399287333 r, 0.3325371741586922 r, 0.3400168541150183 r, 
    0.3475625318359485 r, 0.3551734527599992 r, 0.3628488558014202 r, 
    0.3705879734263036 r, 0.3783900317293359 r, 0.3862542505111889 r, 
    0.3941798433565377 r, 0.4021660177127022 r, 0.4102119749689023 r, 
    0.418316910536117 r, 0.4264800139275439 r, 0.4347004688396462 r, 
    0.4429774532337832 r, 0.451310139418413 r]
    

Berikut kita gambar sikloid untuk r=1.


\>ex &= x-sin(x); ey &= 1-cos(x); aspect(1);

\>plot2d(ex,ey,xmin=0,xmax=4pi,square=1); ...  
\>     plot2d("2+cos(x)","1+sin(x)",xmin=0,xmax=2pi,\>add,color=blue); ...  
\>     plot2d([2,ex(2)],[1,ey(2)],color=red,\>add); ...  
\>     plot2d(ex(2),ey(2),\>points,\>add,color=red); ...  
\>     plot2d("2pi+cos(x)","1+sin(x)",xmin=0,xmax=2pi,\>add,color=blue); ...  
\>     plot2d([2pi,ex(2pi)],[1,ey(2pi)],color=red,\>add);  ...  
\>     plot2d(ex(2pi),ey(2pi),\>points,\>add,color=red):


    Error : [0,1.66665833335744e-7*r-sin(1.66665833335744e-7*r),1.33330666692022e-6*r-sin(1.33330666692022e-6*r),4.499797504338432e-6*r-sin(4.499797504338432e-6*r),1.066581336583994e-5*r-sin(1.066581336583994e-5*r),2.083072932167196e-5*r-sin(2.083072932167196e-5*r),3.599352055540239e-5*r-sin(3.599352055540239e-5*r),5.71526624672386e-5*r-sin(5.71526624672386e-5*r),8.530603082730626e-5*r-sin(8.530603082730626e-5*r),1.214508019889565e-4*r-sin(1.214508019889565e-4*r),1.665833531718508e-4*r-sin(1.665833531718508e-4*r),2.216991628251896e-4*r-sin(2.216991628251896e-4*r),2.877927110806339e-4*r-sin(2.877927110806339e-4*r),3.658573803051457e-4*r-sin(3.658573803051457e-4*r),4.5688535576352e-4*r-sin(4.5688535576352e-4*r),5.618675264007778e-4*r-sin(5.618675264007778e-4*r),6.817933857540259e-4*r-sin(6.817933857540259e-4*r),8.176509330039827e-4*r-sin(8.176509330039827e-4*r),9.704265741758145e-4*r-sin(9.704265741758145e-4*r),0.001141105023499428*r-sin(0.001141105023499428*r),0.001330669204938795*r-sin(0.001330669204938795*r),0.001540100153900437*r-sin(0.001540100153900437*r),0.001770376919130678*r-sin(0.001770376919130678*r),0.002022476464811601*r-sin(0.002022476464811601*r),0.002297373572865413*r-sin(0.002297373572865413*r),0.002596040745477063*r-sin(0.002596040745477063*r),0.002919448107844891*r-sin(0.002919448107844891*r),0.003268563311168871*r-sin(0.003268563311168871*r),0.003644351435886262*r-sin(0.003644351435886262*r),0.004047774895164447*r-sin(0.004047774895164447*r),0.004479793338660443*r-sin(0.004479793338660443*r),0.0049413635565565*r-sin(0.0049413635565565*r),0.005433439383882244*r-sin(0.005433439383882244*r),0.005956971605131645*r-sin(0.005956971605131645*r),0.006512907859185624*r-sin(0.006512907859185624*r),0.007102192544548636*r-sin(0.007102192544548636*r),0.007725766724910044*r-sin(0.007725766724910044*r),0.00838456803503801*r-sin(0.00838456803503801*r),0.009079530587017326*r-sin(0.009079530587017326*r),0.009811584876838586*r-sin(0.009811584876838586*r),0.0105816576913495*r-sin(0.0105816576913495*r),0.01139067201557714*r-sin(0.01139067201557714*r),0.01223954694042984*r-sin(0.01223954694042984*r),0.01312919757078923*r-sin(0.01312919757078923*r),0.01406053493400045*r-sin(0.01406053493400045*r),0.01503446588876983*r-sin(0.01503446588876983*r),0.01605189303448024*r-sin(0.01605189303448024*r),0.01711371462093175*r-sin(0.01711371462093175*r),0.01822082445851714*r-sin(0.01822082445851714*r),0.01937411182884202*r-sin(0.01937411182884202*r),0.02057446139579705*r-sin(0.02057446139579705*r),0.02182275311709253*r-sin(0.02182275311709253*r),0.02311986215626333*r-sin(0.02311986215626333*r),0.02446665879515308*r-sin(0.02446665879515308*r),0.02586400834688696*r-sin(0.02586400834688696*r),0.02731277106934082*r-sin(0.02731277106934082*r),0.02881380207911666*r-sin(0.02881380207911666*r),0.03036795126603076*r-sin(0.03036795126603076*r),0.03197606320812652*r-sin(0.03197606320812652*r),0.0336389770872163*r-sin(0.0336389770872163*r),0.03535752660496472*r-sin(0.03535752660496472*r),0.03713253989951881*r-sin(0.03713253989951881*r),0.03896483946269502*r-sin(0.03896483946269502*r),0.0408552420577305*r-sin(0.0408552420577305*r),0.04280455863760801*r-sin(0.04280455863760801*r),0.04481359426396048*r-sin(0.04481359426396048*r),0.04688314802656623*r-sin(0.04688314802656623*r),0.04901401296344043*r-sin(0.04901401296344043*r),0.05120697598153157*r-sin(0.05120697598153157*r),0.05346281777803219*r-sin(0.05346281777803219*r),0.05578231276230905*r-sin(0.05578231276230905*r),0.05816622897846346*r-sin(0.05816622897846346*r),0.06061532802852698*r-sin(0.06061532802852698*r),0.0631303649963022*r-sin(0.0631303649963022*r),0.06571208837185505*r-sin(0.06571208837185505*r),0.06836123997666599*r-sin(0.06836123997666599*r),0.07107855488944881*r-sin(0.07107855488944881*r),0.07386476137264342*r-sin(0.07386476137264342*r),0.07672058079958999*r-sin(0.07672058079958999*r),0.07964672758239233*r-sin(0.07964672758239233*r),0.08264390910047736*r-sin(0.08264390910047736*r),0.0857128256298576*r-sin(0.0857128256298576*r),0.08885417027310427*r-sin(0.08885417027310427*r),0.09206862889003742*r-sin(0.09206862889003742*r),0.09535688002914089*r-sin(0.09535688002914089*r),0.0987195948597075*r-sin(0.0987195948597075*r),0.1021574371047232*r-sin(0.1021574371047232*r),0.1056710629744951*r-sin(0.1056710629744951*r),0.1092611211010309*r-sin(0.1092611211010309*r),0.1129282524731764*r-sin(0.1129282524731764*r),0.1166730903725168*r-sin(0.1166730903725168*r),0.1204962603100498*r-sin(0.1204962603100498*r),0.1243983799636342*r-sin(0.1243983799636342*r),0.1283800591162231*r-sin(0.1283800591162231*r),0.1324418995948859*r-sin(0.1324418995948859*r),0.1365844952106265*r-sin(0.1365844952106265*r),0.140808431699002*r-sin(0.140808431699002*r),0.1451142866615502*r-sin(0.1451142866615502*r),0.1495026295080298*r-sin(0.1495026295080298*r),0.1539740213994798*r-sin(0.1539740213994798*r)] does not produce a real or column vector
    
    Error generated by error() command
    
    adaptiveeval:
        error(f$|" does not produce a real or column vector"); 
    Try "trace errors" to inspect local variables after errors.
    plot2d:
        dw/n,dw/n^2,dw/n;args());

Berikut dihitung panjang lintasan untuk 1 putaran penuh. (Jangan salah menduga bahwa panjang lintasan 1 putaran penuh sama dengan
keliling lingkaran!)


\>ds &= radcan(sqrt(diff(ex,x)^2+diff(ey,x)^2)); $ds=trigsimp(ds) // elemen panjang kurva sikloid


    Maxima said:
    diff: second argument must be a variable; found errexp1
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    ds &amp;= radcan(sqrt(diff(ex,x)^2+diff(ey,x)^2)); $ds=trigsimp(ds ...
                                                 ^

\>ds &= trigsimp(ds); $ds

\>$showev('integrate(ds,x,0,2\*pi)) // hitung panjang sikloid satu putaran penuh


    Maxima said:
    defint: variable of integration must be a simple or subscripted variable.
    defint: found r*(t-sin(t))
    #0: showev(f='integrate(ds,r*(t-sin(t)),0,2*pi))
     -- an error. To debug this try: debugmode(true);
    
    Error in:
     $showev('integrate(ds,x,0,2*pi)) // hitung panjang sikloid sat ...
                                     ^

\>integrate(mxm("ds"),0,2\*pi) // hitung secara numerik


    Illegal function result in map.
     %evalexpression:
        if maps then return %mapexpression1(x,f$;args());
    gauss:
        if maps then y=%evalexpression(f$,a+h-(h*xn)',maps;args());
    adaptivegauss:
        t1=gauss(f$,c,c+h;args(),=maps);
    Try "trace errors" to inspect local variables after errors.
    integrate:
        return adaptivegauss(f$,a,b,eps*1000;args(),=maps);

\>romberg(mxm("ds"),0,2\*pi) // cara lain hitung secara numerik


    Wrong argument!
    
    Cannot combine a symbolic expression here.
    Did you want to create a symbolic expression?
    Then start with &amp;.
    
    Try "trace errors" to inspect local variables after errors.
    romberg:
        if cols(y)==1 then return y*(b-a); endif;
    Error in:
    romberg(mxm("ds"),0,2*pi) // cara lain hitung secara numerik ...
                             ^

Perhatikan, seperti terlihat pada gambar, panjang sikloid lebih besar daripada keliling lingkarannya, yakni:


## Kurvatur (Kelengkungan) Kurva

image: Osculating.png


Aslinya, kelengkungan kurva diferensiabel (yakni, kurva mulus yang
tidak lancip) di titik P didefinisikan melalui lingkaran oskulasi
(yaitu, lingkaran yang melalui titik P dan terbaik memperkirakan,
paling banyak menyinggung kurva di sekitar P). Pusat dan radius
kelengkungan kurva di P adalah pusat dan radius lingkaran oskulasi.
Kelengkungan adalah kebalikan dari radius kelengkungan:


$$\kappa =\frac {1}{R}$$dengan R adalah radius kelengkungan. (Setiap lingkaran memiliki
kelengkungan ini pada setiap titiknya, dapat diartikan, setiap
lingkaran berputar 2pi sejauh 2piR.)


Definisi ini sulit dimanipulasi dan dinyatakan ke dalam rumus untuk
kurva umum. Oleh karena itu digunakan definisi lain yang ekivalen.


## Definisi Kurvatur dengan Fungsi Parametrik Panjang Kurva



Setiap kurva diferensiabel dapat dinyatakan dengan persamaan
parametrik terhadap panjang kurva s:


$$\gamma(s) = (x(s),\ y(s)),$$dengan x dan y adalah fungsi riil yang diferensiabel, yang memenuhi:


$$\|\gamma'(s)\|=\sqrt{x'(s)^2+y'(s)^2}=1.$$Ini berarti bahwa vektor singgung


$$\mathbf{T}(s)=(x'(s),\ y'(s))$$memiliki norm 1 dan merupakan vektor singgung satuan.


Apabila kurvanya memiliki turunan kedua, artinya turunan kedua x dan y
ada, maka T'(s) ada. Vektor ini merupakan normal kurva yang arahnya
menuju pusat kurvatur, norm-nya merupakan nilai kurvatur
(kelengkungan):


$$ \begin{aligned}\mathbf{T}(s) &= \mathbf{\gamma}'(s),\\ \mathbf{T}^{2}(s) &=1\ \text{(konstanta)}\Rightarrow \mathbf{T}'(s)\cdot \mathbf{T}(s)=0\\ \kappa(s) &=\|\mathbf {T}'(s)\|= \|\mathbf{\gamma}''(s)\|=\sqrt{x''(s)^{2}+y''(s)^{2}}.\end{aligned}$$Nilai


$$R(s)=\frac{1}{\kappa(s)}$$disebut jari-jari (radius) kelengkungan kurva.


Bilangan riil


$$ k(s) = \pm\kappa(s)$$disebut nilai kelengkungan bertanda.


Contoh:


Akan ditentukan kurvatur lingkaran


$$x=r\cos t,\ y= r\sin t.$$\>fx &= r\*cos(t); fy &=r\*sin(t);

\>&assume(t\>0,r\>0); s &=integrate(sqrt(diff(fx,t)^2+diff(fy,t)^2),t,0,t); s // elemen panjang kurva, panjang busur lingkaran (s)


    
                                     r t
    

\>&kill(s); fx &= r\*cos(s/r); fy &=r\*sin(s/r); // definisi ulang persamaan parametrik terhadap s dengan substitusi t=s/r

\>k &= trigsimp(sqrt(diff(fx,s,2)^2+diff(fy,s,2)^2)); $k // nilai kurvatur lingkaran dengan menggunakan definisi di atas


$$\frac{1}{r}$$Untuk representasi parametrik umum, misalkan


$$x = x(t),\ y= y(t)$$merupakan persamaan parametrik untuk kurva bidang yang
terdiferensialkan dua kali. Kurvatur untuk kurva tersebut
didefinisikan sebagai


$$\begin{aligned}\kappa &= \frac{d\phi}{ds}=\frac{\frac{d\phi}{dt}}{\frac{ds}{dt}}\quad (\phi \text{ adalah sudut kemiringan garis singgung dan }s \text{ adalah panjang kurva})\\ &=\frac{\frac{d\phi}{dt}}{\sqrt{(\frac{dx}{dt})^2+(\frac{dy}{dt})^2}}= \frac{\frac{d\phi}{dt}}{\sqrt{x'(t)^2+y'(t)^2}}.\end{aligned}.$$Selanjutnya, pembilang pada persamaan di atas dapat dicari sebagai
berikut.


$$\begin{aligned}\sec^2\phi\frac{d\phi}{dt} &= \frac{d}{dt}\left(\tan\phi\right)= \frac{d}{dt}\left(\frac{dy}{dx}\right)= \frac{d}{dt}\left(\frac{dy/dt}{dx/dt}\right)= \frac{d}{dt}\left(\frac{y'(t)}{x'(t)}\right)=\frac{x'(t)y''(t)-x''(t)y'(t)}{x'(t)^2}.\\ & \\ \frac{d\phi}{dt} &= \frac{1}{\sec^2\phi}\frac{x'(t)y''(t)-x''(t)y'(t)}{x'(t)^2}\\ &= \frac{1}{1+\tan^2\phi}\frac{x'(t)y''(t)-x''(t)y'(t)}{x'(t)^2}\\ &= \frac{1}{1+\left(\frac{y'(t)}{x'(t)}\right)^2}\frac{x'(t)y''(t)-x''(t)y'(t)}{x'(t)^2}\\ &= \frac{x'(t)y''(t)-x''(t)y'(t)}{x'(t)^2+y'(t)^2}.\end{aligned}$$Jadi, rumus kurvatur untuk kurva parametrik


$$x=x(t),\ y=y(t)$$adalah


$$\kappa(t) = \frac{x'(t)y''(t)-x''(t)y'(t)}{\left(x'(t)^2+y'(t)^2\right)^{3/2}}.$$Jika kurvanya dinyatakan dengan persamaan parametrik pada koordinat
kutub


$$x=r(\theta)\cos\theta,\ y=r(\theta)\sin\theta,$$maka rumus kurvaturnya adalah


$$\kappa(\theta) = \frac{r(\theta)^2+2r'(\theta)^2-r(\theta)r''(\theta)}{\left(r'(\theta)^2+r'(\theta)^2\right)^{3/2}}.$$(Silakan Anda turunkan rumus tersebut!)


Contoh:


Lingkaran dengan pusat (0,0) dan jari-jari r dapat dinyatakan dengan
persamaan parametrik


$$x=r\cos t,\ y=r\sin t.$$Nilai kelengkungan lingkaran tersebut adalah


$$\kappa(t)=\frac{x'(t)y''(t)-x''(t)y'(t)}{\left(x'(t)^2+y'(t)^2\right)^{3/2}}=\frac{r^2}{r^3}=\frac 1 r.$$Hasil cocok dengan definisi kurvatur suatu kelengkungan.


Kurva


$$y=f(x)$$dapat dinyatakan ke dalam persamaan parametrik


$$x=t,\ y=f(t),\ \text{ dengan } x'(t)=1,\ x''(t)=0,$$sehingga kurvaturnya adalah


$$\kappa(t) = \frac{y''(t)}{\left(1+y'(t)^2\right)^{3/2}}.$$Contoh:


Akan ditentukan kurvatur parabola


$$y=ax^2+bx+c.$$\>function f(x) &= a\*x^2+b\*x+c; $y=f(x)


$$r\,\left(1-\cos t\right)=b\,r\,\left(t-\sin t\right)+a\,r^2\,\left(  t-\sin t\right)^2+c$$\>function k(x) &= (diff(f(x),x,2))/(1+diff(f(x),x)^2)^(3/2); $'k(x)=k(x) // kelengkungan parabola 


    Maxima said:
    diff: second argument must be a variable; found r*(t-sin(t))
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    ... (x) &amp;= (diff(f(x),x,2))/(1+diff(f(x),x)^2)^(3/2); $'k(x)=k(x)  ...
                                                         ^

\>function f(x) &= x^2+x+1; $y=f(x) // akan kita plot kelengkungan parabola untuk a=b=c=1


$$r\,\left(1-\cos t\right)=r\,\left(t-\sin t\right)+r^2\,\left(t-  \sin t\right)^2+1$$\>function k(x) &= (diff(f(x),x,2))/(1+diff(f(x),x)^2)^(3/2); $'k(x)=k(x) // kelengkungan parabola 


    Maxima said:
    diff: second argument must be a variable; found r*(t-sin(t))
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    ... (x) &amp;= (diff(f(x),x,2))/(1+diff(f(x),x)^2)^(3/2); $'k(x)=k(x)  ...
                                                         ^

Berikut kita gambar parabola tersebut beserta kurva kelengkungan, kurva jari-jari kelengkungan dan salah satu lingkaran oskulasi
di titik puncak parabola. Perhatikan, puncak parabola dan jari-jari lingkaran oskulasi di puncak parabola adalah


sehingga pusat lingkaran oskulasi adalah (-1/2, 5/4).


\>plot2d(["f(x)", "k(x)"],-2,1, color=[blue,red]); plot2d("1/k(x)",-1.5,1,color=green,\>add); ...  
\>   plot2d("-1/2+1/k(-1/2)\*cos(x)","5/4+1/k(-1/2)\*sin(x)",xmin=0,xmax=2pi,\>add,color=blue):


    Variable or function t not found.
    f:
        useglobal; return r*(t-sin(t))+r^2*(t-sin(t))^2+1 
    Error in expression: f(x)
     %ploteval:
        y0=f$(x[1],args());
    adaptiveevalone:
        s=%ploteval(g$,t;args());
    Try "trace errors" to inspect local variables after errors.
    plot2d:
        dw/n,dw/n^2,dw/n,auto;args());

Untuk kurva yang dinyatakan dengan fungsi implisit


dengan turunan-turunan parsial


berlaku


sehingga kurvaturnya adalah


(Silakan Anda turunkan sendiri!)


Contoh 1:


Parabola 


dapat dinyatakan ke dalam persamaan implisit


\>function F(x,y) &=a\*x^2+b\*x+c-y; $F(x,y)


$$b\,r\,\left(t-\sin t\right)+a\,r^2\,\left(t-\sin t\right)^2-r\,  \left(1-\cos t\right)+c$$\>Fx &= diff(F(x,y),x), Fxx &=diff(F(x,y),x,2), Fy &=diff(F(x,y),y), Fxy &=diff(diff(F(x,y),x),y), Fyy &=diff(F(x,y),y,2)  


    Maxima said:
    diff: second argument must be a variable; found r*(t-sin(t))
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    Fx &amp;= diff(F(x,y),x), Fxx &amp;=diff(F(x,y),x,2), Fy &amp;=diff(F(x,y) ...
                        ^

\>function k(x) &= (Fy^2\*Fxx-2\*Fx\*Fy\*Fxy+Fx^2\*Fyy)/(Fx^2+Fy^2)^(3/2); $'k(x)=k(x) // kurvatur parabola tersebut


$$k\left(r\,\left(t-\sin t\right)\right)=\frac{{\it Fx}^2\,{\it Fyy}+  {\it Fxx}\,{\it Fy}^2-2\,{\it Fx}\,{\it Fxy}\,{\it Fy}}{\left(  {\it Fy}^2+{\it Fx}^2\right)^{\frac{3}{2}}}$$Hasilnya sama dengan sebelumnya yang menggunakan persamaan parabola biasa.


# Latihan

* 
Bukalah buku Kalkulus.

* 
Cari dan pilih beberapa (paling sedikit 5 fungsi berbeda tipe/bentuk/jenis) fungsi dari buku tersebut, kemudian definisikan di
* EMT pada baris-baris perintah berikut (jika perlu tambahkan lagi).

* 
Untuk setiap fungsi, tentukan anti turunannya (jika ada), hitunglah integral tentu dengan batas-batas yang menarik (Anda
* tentukan sendiri), seperti contoh-contoh tersebut.

* 
Lakukan hal yang sama untuk fungsi-fungsi yang tidak dapat diintegralkan (cari sedikitnya 3 fungsi).

* 
Gambar grafik fungsi dan daerah integrasinya pada sumbu koordinat yang sama.

* 
Gunakan integral tentu untuk mencari luas daerah yang dibatasi oleh dua kurva yang berpotongan di dua titik. (Cari dan gambar
* kedua kurva dan arsir (warnai) daerah yang dibatasi oleh keduanya.)

* 
Gunakan integral tentu untuk menghitung volume benda putar kurva y= f(x) yang diputar mengelilingi sumbu x dari x=a sampai x=b,
* yakni


(Pilih fungsinya dan gambar kurva dan benda putar yang dihasilkan. Anda dapat mencari contoh-contoh bagaimana cara menggambar
benda hasil perputaran suatu kurva.)


- Gunakan integral tentu untuk menghitung panjang kurva y=f(x) dari x=a sampai x=b dengan menggunakan rumus:


(Pilih fungsi dan gambar kurvanya.)


- Apabila fungsi dinyatakan dalam koordinat kutub x=f(r,t), y=g(r,t), r=h(t), x=a bersesuaian dengan t=t0 dan x=b bersesuian
dengan t=t1, maka rumus di atas akan menjadi:


* 
Pilih beberapa kurva menarik (selain lingkaran dan parabola) dari buku  kalkulus. Nyatakan setiap kurva tersebut dalam bentuk:
*   a. koordinat Kartesius (persamaan y=f(x))
*   b. koordinat kutub ( r=r(theta))
*   c. persamaan parametrik x=x(t), y=y(t)
*   d. persamaan implit F(x,y)=0

* 
Tentukan kurvatur masing-masing kurva dengan menggunakan keempat representasi tersebut (hasilnya harus sama).

* 
Gambarlah kurva asli, kurva kurvatur, kurva jari-jari lingkaran oskulasi, dan salah satu lingkaran oskulasinya.


# Barisan dan Deret

(Catatan: bagian ini belum lengkap. Anda dapat membaca contoh-contoh pengguanaan EMT dan
Maxima untuk menghitung limit barisan, rumus jumlah parsial suatu deret, jumlah tak hingga
suatu deret konvergen, dan sebagainya. Anda dapat mengeksplor contoh-contoh di EMT atau
perbagai panduan penggunaan Maxima di software Maxima atau dari Internet.)


Barisan dapat didefinisikan dengan beberapa cara di dalam EMT, di antaranya:


* 
dengan cara yang sama seperti mendefinisikan vektor dengan elemen-elemen beraturan
* (menggunakan titik dua ":");

* 
menggunakan perintah "sequence" dan rumus barisan (suku ke -n);

* 
menggunakan perintah "iterate" atau "niterate";

* 
menggunakan fungsi Maxima "create_list" atau "makelist" untuk menghasilkan barisan
* simbolik;

* 
menggunakan fungsi biasa yang inputnya vektor atau barisan;

* 
menggunakan fungsi rekursif.


EMT menyediakan beberapa perintah (fungsi) terkait barisan, yakni:


* 
sum: menghitung jumlah semua elemen suatu barisan

* 
cumsum: jumlah kumulatif suatu barisan

* 
differences: selisih antar elemen-elemen berturutan


EMT juga dapat digunakan untuk menghitung jumlah deret berhingga maupun deret tak hingga,
dengan menggunakan perintah (fungsi) "sum". Perhitungan dapat dilakukan secara numerik
maupun simbolik dan eksak.


Berikut adalah beberapa contoh perhitungan barisan dan deret menggunakan EMT.


\>1:10 // barisan sederhana


    [1,  2,  3,  4,  5,  6,  7,  8,  9,  10]

\>1:2:30


    [1,  3,  5,  7,  9,  11,  13,  15,  17,  19,  21,  23,  25,  27,  29]

# Iterasi dan Barisan

EMT menyediakan fungsi iterate("g(x)", x0, n) untuk melakukan iterasi


$$x_{k+1}=g(x_k), \ x_0=x_0, k= 1, 2, 3, ..., n.$$Berikut ini disajikan contoh-contoh penggunaan iterasi dan rekursi
dengan EMT. Contoh pertama menunjukkan pertumbuhan dari nilai awal
1000 dengan laju pertambahan 5%, selama 10 periode.


\>q=1.05; iterate("x\*q",1000,n=10)'


             1000 
             1050 
           1102.5 
          1157.63 
          1215.51 
          1276.28 
           1340.1 
           1407.1 
          1477.46 
          1551.33 
          1628.89 

Contoh berikutnya memperlihatkan bahaya menabung di bank pada masa sekarang! Dengan bunga
tabungan sebesar 6% per tahun atau 0.5% per bulan dipotong pajak 20%, dan biaya administrasi
10000 per bulan, tabungan sebesar 1 juta tanpa diambil selama sekitar 10 tahunan akan habis
diambil oleh bank!


\>r=0.005; plot2d(iterate("(1+0.8\*r)\*x-10000",1000000,n=130)):


![images/EMT4Kalkulus%20(1)-284.png](images/EMT4Kalkulus%20(1)-284.png)

Silakan Anda coba-coba, dengan tabungan minimal berapa agar tidak akan habis diambil oleh
bank dengan ketentuan bunga dan biaya administrasi seperti di atas.


Berikut adalah perhitungan minimal tabungan agar aman di bank dengan bunga sebesar r dan
biaya administrasi a, pajak bunga 20%.


\>$solve(0.8\*r\*A-a,A), $% with [r=0.005, a=10] 


$$\left[ A=2500.0 \right] $$![images/EMT4Kalkulus%20(1)-286.png](images/EMT4Kalkulus%20(1)-286.png)

Berikut didefinisikan fungsi untuk menghitung saldo tabungan, kemudian dilakukan iterasi.


\>function saldo(x,r,a) := round((1+0.8\*r)\*x-a,2);

\>iterate({{"saldo",0.005,10}},1000,n=6)


    [1000,  994,  987.98,  981.93,  975.86,  969.76,  963.64]

\>iterate({{"saldo",0.005,10}},2000,n=6)


    [2000,  1998,  1995.99,  1993.97,  1991.95,  1989.92,  1987.88]

\>iterate({{"saldo",0.005,10}},2500,n=6)


    [2500,  2500,  2500,  2500,  2500,  2500,  2500]

Tabungan senilai 2,5 juta akan aman dan tidak akan berubah nilai (jika tidak ada penarikan),
sedangkan jika tabungan awal kurang dari 2,5 juta, lama kelamaan akan berkurang meskipun
tidak pernah dilakukan penarikan uang tabungan.


\>iterate({{"saldo",0.005,10}},3000,n=6)


    [3000,  3002,  3004.01,  3006.03,  3008.05,  3010.08,  3012.12]

Tabungan yang lebih dari 2,5 juta baru akan bertambah jika tidak ada
penarikan.


Untuk barisan yang lebih kompleks dapat digunakan fungsi "sequence()".
Fungsi ini menghitung nilai-nilai x[n] dari semua nilai sebelumnya,
x[1],...,x[n-1] yang diketahui.


Berikut adalah contoh barisan Fibonacci.


$$x_n = x_{n-1}+x_{n-2}, \quad x_1=1, \quad x_2 =1$$\>sequence("x[n-1]+x[n-2]",[1,1],15)


    [1,  1,  2,  3,  5,  8,  13,  21,  34,  55,  89,  144,  233,  377,  610]

Barisan Fibonacci memiliki banyak sifat menarik, salah satunya adalah akar pangkat ke-n suku
ke-n akan konvergen ke pecahan emas:


\>$'(1+sqrt(5))/2=float((1+sqrt(5))/2)


$$\frac{\sqrt{5}+1}{2}=1.618033988749895$$\>plot2d(sequence("x[n-1]+x[n-2]",[1,1],250)^(1/(1:250))):


![images/EMT4Kalkulus%20(1)-289.png](images/EMT4Kalkulus%20(1)-289.png)

Barisan yang sama juga dapat dihasilkan dengan menggunakan loop.


\>x=ones(500); for k=3 to 500; x[k]=x[k-1]+x[k-2]; end;


Rekursi dapat dilakukan dengan menggunakan rumus yang tergantung pada semua elemen
sebelumnya. Pada contoh berikut, elemen ke-n merupakan jumlah (n-1) elemen sebelumnya,
dimulai dengan 1 (elemen ke-1). Jelas, nilai elemen ke-n adalah 2^(n-2), untuk n=2, 4, 5,
....


\>sequence("sum(x)",1,10)


    [1,  1,  2,  4,  8,  16,  32,  64,  128,  256]

Selain menggunakan ekspresi dalam x dan n, kita juga dapat menggunakan
fungsi.


Pada contoh berikut, digunakan iterasi


$$x_n =A \cdot x_{n-1},$$dengan A suatu matriks 2x2, dan setiap x[n] merupakan matriks/vektor
2x1.


\>A=[1,1;1,2]; function suku(x,n) := A.x[,n-1]

\>sequence("suku",[1;1],6)


    Real 2 x 6 matrix
    
                1             2             5            13     ...
                1             3             8            21     ...

Hasil yang sama juga dapat diperoleh dengan menggunakan fungsi
perpangkatan matriks "matrixpower()". Cara ini lebih cepat, karena
hanya menggunakan perkalian matriks sebanyak log_2(n).


$$x_n=A.x_{n-1}=A^2.x_{n-2}=A^3.x_{n-3}= ... = A^{n-1}.x_1.$$\>sequence("matrixpower(A,n).[1;1]",1,6)


    Real 2 x 6 matrix
    
                1             5            13            34     ...
                1             8            21            55     ...

# Spiral Theodorus

image: Spiral_of_Theodorus.png


Spiral Theodorus (spiral segitiga siku-siku) dapat digambar secara
rekursif. Rumus rekursifnya adalah:


$$x_n = \left( 1 + \frac{i}{\sqrt{n-1}} \right) \, x_{n-1}, \quad x_1=1,$$yang menghasilkan barisan bilangan kompleks.


\>function g(n) := 1+I/sqrt(n)


Rekursinya dapat dijalankan sebanyak 17 untuk menghasilkan barisan 17 bilangan kompleks,
kemudian digambar bilangan-bilangan kompleksnya.


\>x=sequence("g(n-1)\*x[n-1]",1,17); plot2d(x,r=3.5); textbox(latex("Spiral\\ Theodorus"),0.4):


![images/EMT4Kalkulus%20(1)-293.png](images/EMT4Kalkulus%20(1)-293.png)

Selanjutnya dihubungan titik 0 dengan titik-titik kompleks tersebut menggunakan loop.


\>for i=1:cols(x); plot2d([0,x[i]],\>add); end:


![images/EMT4Kalkulus%20(1)-294.png](images/EMT4Kalkulus%20(1)-294.png)

\> 


Spiral tersebut juga dapat didefinisikan menggunakan fungsi rekursif, yang tidak memmerlukan
indeks dan bilangan kompleks. Dalam hal ini diigunakan vektor kolom pada bidang.


\>function gstep (v) ...


    w=[-v[2];v[1]];
    return v+w/norm(w);
    endfunction
</pre>
Jika dilakukan iterasi 16 kali dimulai dari [1;0] akan didapatkan matriks yang memuat
vektor-vektor dari setiap iterasi.


\>x=iterate("gstep",[1;0],16); plot2d(x[1],x[2],r=3.5,\>points):


![images/EMT4Kalkulus%20(1)-295.png](images/EMT4Kalkulus%20(1)-295.png)

# Kekonvergenan

Terkadang kita ingin melakukan iterasi sampai konvergen. Apabila iterasinya tidak konvergen
setelah ditunggu lama, Anda dapat menghentikannya dengan menekan tombol [ESC].


\>iterate("cos(x)",1) // iterasi x(n+1)=cos(x(n)), dengan x(0)=1.


    0.739085133216

Iterasi tersebut konvergen ke penyelesaian persamaan


Iterasi ini juga dapat dilakukan pada interval, hasilnya adalah barisan interval yang memuat
akar tersebut.


\>hasil := iterate("cos(x)",~1,2~) //iterasi x(n+1)=cos(x(n)), dengan interval awal (1, 2)


    ~0.739085133211,0.7390851332133~

Jika interval hasil tersebut sedikit diperlebar, akan terlihat bahwa interval tersebut
memuat akar persamaan x=cos(x).


\>h=expand(hasil,100), cos(h) << h


    ~0.73908513309,0.73908513333~
    1

Iterasi juga dapat digunakan pada fungsi yang didefinisikan.


\>function f(x) := (x+2/x)/2


Iterasi x(n+1)=f(x(n)) akan konvergen ke akar kuadrat 2.


\>iterate("f",2), sqrt(2)


    1.41421356237
    1.41421356237

Jika pada perintah iterate diberikan tambahan parameter n, maka hasil iterasinya akan
ditampilkan mulai dari iterasi pertama sampai ke-n.


\>iterate("f",2,5)


    [2,  1.5,  1.41667,  1.41422,  1.41421,  1.41421]

Untuk iterasi ini tidak dapat dilakukan terhadap interval.


\>niterate("f",~1,2~,5)


    [ ~1,2~,  ~1,2~,  ~1,2~,  ~1,2~,  ~1,2~,  ~1,2~ ]

Perhatikan, hasil iterasinya sama dengan interval awal. Alasannya adalah perhitungan dengan
interval bersifat terlalu longgar. Untuk meingkatkan perhitungan pada ekspresi dapat
digunakan pembagian intervalnya, menggunakan fungsi ieval().


\>function s(x) := ieval("(x+2/x)/2",x,10)


Selanjutnya dapat dilakukan iterasi hingga diperoleh hasil optimal,
dan intervalnya tidak semakin mengecil. Hasilnya berupa interval yang
memuat akar persamaan:


$$x = \frac{1}{2} \left( x + \frac{2}{x} \right).$$Satu-satunya solusi adalah


$$x = \sqrt2.$$\>iterate("s",~1,2~)


    ~1.41421356236,1.41421356239~

Fungsi "iterate()" juga dapat bekerja pada vektor. Berikut adalah
contoh fungsi vektor, yang menghasilkan rata-rata aritmetika dan
rata-rata geometri.


$$(a_{n+1},b_{n+1}) = \left( \frac{a_n+b_n}{2}, \sqrt{a_nb_n} \right)$$Iterasi ke-n disimpan pada vektor kolom x[n].


\>function g(x) := [(x[1]+x[2])/2;sqrt(x[1]\*x[2])]


Iterasi dengan menggunakan fungsi tersebut akan konvergen ke rata-rata aritmetika dan
geometri dari nilai-nilai awal. 


\>iterate("g",[1;5])


          2.60401 
          2.60401 

Hasil tersebut konvergen agak cepat, seperti kita cek sebagai berikut.


\>iterate("g",[1;5],4)


                1             3       2.61803       2.60403       2.60401 
                5       2.23607       2.59002       2.60399       2.60401 

Iterasi pada interval dapat dilakukan dan stabil, namun tidak menunjukkan bahwa limitnya
pada batas-batas yang dihitung.


\>iterate("g",[~1~;~5~],4)


    Interval 2 x 5 matrix
    
    ~0.999999999999999778,1.00000000000000022~     ...
    ~4.99999999999999911,5.00000000000000089~     ...

Iterasi berikut konvergen sangat lambat.


$$x_{n+1} = \sqrt{x_n}.$$\>iterate("sqrt(x)",2,10)


    [2,  1.41421,  1.18921,  1.09051,  1.04427,  1.0219,  1.01089,
    1.00543,  1.00271,  1.00135,  1.00068]

Kekonvergenan iterasi tersebut dapat dipercepatdengan percepatan Steffenson:


\>steffenson("sqrt(x)",2,10)


    [1.04888,  1.00028,  1,  1]

# Iterasi menggunakan Loop yang ditulis Langsung

Berikut adalah beberapa contoh penggunaan loop untuk melakukan iterasi yang ditulis langsung
pada baris perintah.


\>x=2; repeat x=(x+2/x)/2; until x^2~=2; end; x,


    1.41421356237

Penggabungan matriks menggunakan tanda "|" dapat digunakan untuk menyimpan semua hasil
iterasi.


\>v=[1]; for i=2 to 8; v=v|(v[i-1]\*i); end; v,


    [1,  2,  6,  24,  120,  720,  5040,  40320]

hasil iterasi juga dapat disimpan pada vektor yang sudah ada.


\>v=ones(1,100); for i=2 to cols(v); v[i]=v[i-1]\*i; end; ...  
\>   plot2d(v,logplot=1); textbox(latex(&log(n)),x=0.5):


![images/EMT4Kalkulus%20(1)-300.png](images/EMT4Kalkulus%20(1)-300.png)

\>A =[0.5,0.2;0.7,0.1]; b=[2;2]; ...  
\>   x=[1;1]; repeat xnew=A.x-b; until all(xnew~=x); x=xnew; end; ...  
\>   x,


         -7.09677 
         -7.74194 

# Iterasi di dalam Fungsi

Fungsi atau program juga dapat menggunakan iterasi dan dapat digunakan untuk melakukan iterasi. Berikut adalah beberapa contoh
iterasi di dalam fungsi.


Contoh berikut adalah suatu fungsi untuk menghitung berapa lama suatu iterasi konvergen. Nilai fungsi tersebut adalah hasil akhir
iterasi dan banyak iterasi sampai konvergen.


\>function map hiter(f$,x0) ...


    x=x0;
    maxiter=0;
    repeat
      xnew=f$(x);
      maxiter=maxiter+1;
      until xnew~=x;
      x=xnew;
    end;
    return maxiter;
    endfunction
</pre>
Misalnya, berikut adalah iterasi untuk mendapatkan hampiran akar kuadrat 2, cukup cepat,
konvergen pada iterasi ke-5, jika dimulai dari hampiran awal 2.


\>hiter("(x+2/x)/2",2)


    5

Karena fungsinya didefinisikan menggunakan "map". maka nilai awalnya dapat berupa vektor.


\>x=1.5:0.1:10; hasil=hiter("(x+2/x)/2",x); ...  
\>     plot2d(x,hasil):


![images/EMT4Kalkulus%20(1)-301.png](images/EMT4Kalkulus%20(1)-301.png)

Dari gambar di atas terlihat bahwa kekonvergenan iterasinya semakin lambat, untuk nilai awal
semakin besar, namun penambahnnya tidak kontinu. Kita dapat menemukan kapan maksimum
iterasinya bertambah.


\>hasil[1:10]


    [4,  5,  5,  5,  5,  5,  6,  6,  6,  6]

\>x[nonzeros(differences(hasil))]


    [1.5,  2,  3.4,  6.6]

maksimum iterasi sampai konvergen meningkat pada saat nilai awalnya 1.5, 2, 3.4, dan 6.6.


Contoh berikutnya adalah metode Newton pada polinomial kompleks berderajat 3.


\>p &= x^3-1; newton &= x-p/diff(p,x); $newton


    Maxima said:
    diff: second argument must be a variable; found errexp1
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    p &amp;= x^3-1; newton &amp;= x-p/diff(p,x); $newton ...
                                       ^

Selanjutnya didefinisikan fungsi untuk melakukan iterasi (aslinya 10 kali).


\>function iterasi(f$,x,n=10) ...


    loop 1 to n; x=f$(x); end;
    return x;
    endfunction
</pre>
Kita mulai dengan menentukan titik-titik grid pada bidang kompleksnya.


\>r=1.5; x=linspace(-r,r,501); Z=x+I\*x'; W=iterasi(newton,Z);


    Function newton needs at least 3 arguments!
    Use: newton (f$: call, df$: call, x: scalar complex {, y: number, eps: none}) 
    Error in:
    ...  x=linspace(-r,r,501); Z=x+I*x'; W=iterasi(newton,Z); ...
                                                         ^

Berikut adalah akar-akar polinomial di atas.


\>z=&solve(p)()


    Maxima said:
    solve: more equations than unknowns.
    Unknowns given :  
    [r]
    Equations given:  
    errexp1
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    z=&amp;solve(p)() ...
               ^

Untuk menggambar hasil iterasinya, dihitung jarak dari hasil iterasi ke-10 ke masing-masing
akar, kemudian digunakan untuk menghitung warna yang akan digambar, yang menunjukkan limit
untuk masing-masing nilai awal. 


Fungsi plotrgb() menggunakan jendela gambar terkini untuk menggambar warna RGB sebagai
matriks.


\>C=rgb(max(abs(W-z[1]),1),max(abs(W-z[2]),1),max(abs(W-z[3]),1)); ...  
\>     plot2d(none,-r,r,-r,r); plotrgb(C):


    Variable W not found!
    Error in:
    C=rgb(max(abs(W-z[1]),1),max(abs(W-z[2]),1),max(abs(W-z[3]),1) ...
                        ^

# Iterasi Simbolik

Seperti sudah dibahas sebelumnya, untuk menghasilkan barisan ekspresi simbolik dengan Maxima
dapat digunakan fungsi makelist().


\>&powerdisp:true // untuk menampilkan deret pangkat mulai dari suku berpangkat terkecil


    
                                     true
    

\>deret &= makelist(taylor(exp(x),x,0,k),k,1,3); $deret // barisan deret Taylor untuk e^x


    Maxima said:
    taylor: 0.1539740213994798*r cannot be a variable.
     -- an error. To debug this try: debugmode(true);
    
    Error in:
    deret &amp;= makelist(taylor(exp(x),x,0,k),k,1,3); $deret // baris ...
                                                 ^

Untuk mengubah barisan deret tersebut menjadi vektor string di EMT digunakan fungsi
mxm2str(). Selanjutnya, vektor string/ekspresi hasilnya dapat digambar seperti menggambar
vektor eskpresi pada EMT.


\>plot2d("exp(x)",0,3); // plot fungsi aslinya, e^x

\>plot2d(mxm2str("deret"),\>add,color=4:6): // plot ketiga deret taylor hampiran fungsi tersebut


    Maxima said:
    length: argument cannot be a symbol; found deret
     -- an error. To debug this try: debugmode(true);
    
    mxmeval:
        return evaluate(mxm(s));
    Try "trace errors" to inspect local variables after errors.
    mxm2str:
        n=mxmeval("length(VVV)");

Selain cara di atas dapat juga dengan cara menggunakan indeks pada vektor/list yang
dihasilkan.


\>$deret[3]


$${\it deret}_{3}$$\>plot2d(["exp(x)",&deret[1],&deret[2],&deret[3]],0,3,color=1:4):


    deret is not a variable!
    Error in expression: deret[1]
     %ploteval:
        y0=f$(x[1],args());
    Try "trace errors" to inspect local variables after errors.
    plot2d:
        u=u_(%ploteval(xx[#],t;args()));

\>$sum(sin(k\*x)/k,k,1,5)


$$\left[ 0 , \sin \left(1.66665833335744 \times 10^{-7}\,r\right)+  \frac{\sin \left(3.333316666714881 \times 10^{-7}\,r\right)}{2}+  \frac{\sin \left(4.999975000072321 \times 10^{-7}\,r\right)}{3}+  \frac{\sin \left(6.666633333429761 \times 10^{-7}\,r\right)}{4}+  \frac{\sin \left(8.333291666787201 \times 10^{-7}\,r\right)}{5} ,   \sin \left(1.33330666692022 \times 10^{-6}\,r\right)+\frac{\sin   \left(2.66661333384044 \times 10^{-6}\,r\right)}{2}+\frac{\sin   \left(3.999920000760659 \times 10^{-6}\,r\right)}{3}+\frac{\sin   \left(5.333226667680879 \times 10^{-6}\,r\right)}{4}+\frac{\sin   \left(6.666533334601099 \times 10^{-6}\,r\right)}{5} , \sin \left(  4.499797504338432 \times 10^{-6}\,r\right)+\frac{\sin \left(  8.999595008676864 \times 10^{-6}\,r\right)}{2}+\frac{\sin \left(  1.34993925130153 \times 10^{-5}\,r\right)}{3}+\frac{\sin \left(  1.799919001735373 \times 10^{-5}\,r\right)}{4}+\frac{\sin \left(  2.249898752169216 \times 10^{-5}\,r\right)}{5} , \sin \left(  1.066581336583994 \times 10^{-5}\,r\right)+\frac{\sin \left(  2.133162673167988 \times 10^{-5}\,r\right)}{2}+\frac{\sin \left(  3.199744009751981 \times 10^{-5}\,r\right)}{3}+\frac{\sin \left(  4.266325346335975 \times 10^{-5}\,r\right)}{4}+\frac{\sin \left(  5.332906682919969 \times 10^{-5}\,r\right)}{5} , \sin \left(  2.083072932167196 \times 10^{-5}\,r\right)+\frac{\sin \left(  4.166145864334392 \times 10^{-5}\,r\right)}{2}+\frac{\sin \left(  6.249218796501588 \times 10^{-5}\,r\right)}{3}+\frac{\sin \left(  8.332291728668784 \times 10^{-5}\,r\right)}{4}+\frac{\sin \left(  1.041536466083598 \times 10^{-4}\,r\right)}{5} , \sin \left(  3.599352055540239 \times 10^{-5}\,r\right)+\frac{\sin \left(  7.198704111080478 \times 10^{-5}\,r\right)}{2}+\frac{\sin \left(  1.079805616662072 \times 10^{-4}\,r\right)}{3}+\frac{\sin \left(  1.439740822216096 \times 10^{-4}\,r\right)}{4}+\frac{\sin \left(  1.79967602777012 \times 10^{-4}\,r\right)}{5} , \sin \left(  5.71526624672386 \times 10^{-5}\,r\right)+\frac{\sin \left(  1.143053249344772 \times 10^{-4}\,r\right)}{2}+\frac{\sin \left(  1.714579874017158 \times 10^{-4}\,r\right)}{3}+\frac{\sin \left(  2.286106498689544 \times 10^{-4}\,r\right)}{4}+\frac{\sin \left(  2.85763312336193 \times 10^{-4}\,r\right)}{5} , \sin \left(  8.530603082730626 \times 10^{-5}\,r\right)+\frac{\sin \left(  1.706120616546125 \times 10^{-4}\,r\right)}{2}+\frac{\sin \left(  2.559180924819188 \times 10^{-4}\,r\right)}{3}+\frac{\sin \left(  3.41224123309225 \times 10^{-4}\,r\right)}{4}+\frac{\sin \left(  4.265301541365313 \times 10^{-4}\,r\right)}{5} , \sin \left(  1.214508019889565 \times 10^{-4}\,r\right)+\frac{\sin \left(  2.42901603977913 \times 10^{-4}\,r\right)}{2}+\frac{\sin \left(  3.643524059668696 \times 10^{-4}\,r\right)}{3}+\frac{\sin \left(  4.858032079558261 \times 10^{-4}\,r\right)}{4}+\frac{\sin \left(  6.072540099447826 \times 10^{-4}\,r\right)}{5} , \sin \left(  1.665833531718508 \times 10^{-4}\,r\right)+\frac{\sin \left(  3.331667063437016 \times 10^{-4}\,r\right)}{2}+\frac{\sin \left(  4.997500595155524 \times 10^{-4}\,r\right)}{3}+\frac{\sin \left(  6.663334126874032 \times 10^{-4}\,r\right)}{4}+\frac{\sin \left(  8.32916765859254 \times 10^{-4}\,r\right)}{5} , \sin \left(  2.216991628251896 \times 10^{-4}\,r\right)+\frac{\sin \left(  4.433983256503793 \times 10^{-4}\,r\right)}{2}+\frac{\sin \left(  6.650974884755689 \times 10^{-4}\,r\right)}{3}+\frac{\sin \left(  8.867966513007586 \times 10^{-4}\,r\right)}{4}+\frac{\sin \left(  0.001108495814125948\,r\right)}{5} , \sin \left(  2.877927110806339 \times 10^{-4}\,r\right)+\frac{\sin \left(  5.755854221612677 \times 10^{-4}\,r\right)}{2}+\frac{\sin \left(  8.633781332419016 \times 10^{-4}\,r\right)}{3}+\frac{\sin \left(  0.001151170844322535\,r\right)}{4}+\frac{\sin \left(  0.001438963555403169\,r\right)}{5} , \sin \left(  3.658573803051457 \times 10^{-4}\,r\right)+\frac{\sin \left(  7.317147606102914 \times 10^{-4}\,r\right)}{2}+\frac{\sin \left(  0.001097572140915437\,r\right)}{3}+\frac{\sin \left(  0.001463429521220583\,r\right)}{4}+\frac{\sin \left(  0.001829286901525728\,r\right)}{5} , \sin \left(  4.568853557635201 \times 10^{-4}\,r\right)+\frac{\sin \left(  9.137707115270399 \times 10^{-4}\,r\right)}{2}+\frac{\sin \left(  0.00137065606729056\,r\right)}{3}+\frac{\sin \left(  0.00182754142305408\,r\right)}{4}+\frac{\sin \left(  0.0022844267788176\,r\right)}{5} , \sin \left(  5.618675264007778 \times 10^{-4}\,r\right)+\frac{\sin \left(  0.001123735052801556\,r\right)}{2}+\frac{\sin \left(  0.001685602579202333\,r\right)}{3}+\frac{\sin \left(  0.002247470105603111\,r\right)}{4}+\frac{\sin \left(  0.002809337632003889\,r\right)}{5} , \sin \left(  6.817933857540259 \times 10^{-4}\,r\right)+\frac{\sin \left(  0.001363586771508052\,r\right)}{2}+\frac{\sin \left(  0.002045380157262078\,r\right)}{3}+\frac{\sin \left(  0.002727173543016104\,r\right)}{4}+\frac{\sin \left(  0.00340896692877013\,r\right)}{5} , \sin \left(  8.176509330039827 \times 10^{-4}\,r\right)+\frac{\sin \left(  0.001635301866007965\,r\right)}{2}+\frac{\sin \left(  0.002452952799011948\,r\right)}{3}+\frac{\sin \left(  0.003270603732015931\,r\right)}{4}+\frac{\sin \left(  0.004088254665019914\,r\right)}{5} , \sin \left(  9.704265741758145 \times 10^{-4}\,r\right)+\frac{\sin \left(  0.001940853148351629\,r\right)}{2}+\frac{\sin \left(  0.002911279722527443\,r\right)}{3}+\frac{\sin \left(  0.003881706296703258\,r\right)}{4}+\frac{\sin \left(  0.004852132870879072\,r\right)}{5} , \sin \left(0.001141105023499428  \,r\right)+\frac{\sin \left(0.002282210046998856\,r\right)}{2}+  \frac{\sin \left(0.003423315070498284\,r\right)}{3}+\frac{\sin   \left(0.004564420093997712\,r\right)}{4}+\frac{\sin \left(  0.00570552511749714\,r\right)}{5} , \sin \left(0.001330669204938795  \,r\right)+\frac{\sin \left(0.002661338409877589\,r\right)}{2}+  \frac{\sin \left(0.003992007614816384\,r\right)}{3}+\frac{\sin   \left(0.005322676819755179\,r\right)}{4}+\frac{\sin \left(  0.006653346024693974\,r\right)}{5} , \sin \left(0.001540100153900437  \,r\right)+\frac{\sin \left(0.003080200307800873\,r\right)}{2}+  \frac{\sin \left(0.00462030046170131\,r\right)}{3}+\frac{\sin \left(  0.006160400615601747\,r\right)}{4}+\frac{\sin \left(  0.007700500769502183\,r\right)}{5} , \sin \left(0.001770376919130678  \,r\right)+\frac{\sin \left(0.003540753838261357\,r\right)}{2}+  \frac{\sin \left(0.005311130757392035\,r\right)}{3}+\frac{\sin   \left(0.007081507676522714\,r\right)}{4}+\frac{\sin \left(  0.008851884595653392\,r\right)}{5} , \sin \left(0.002022476464811601  \,r\right)+\frac{\sin \left(0.004044952929623202\,r\right)}{2}+  \frac{\sin \left(0.006067429394434803\,r\right)}{3}+\frac{\sin   \left(0.008089905859246405\,r\right)}{4}+\frac{\sin \left(  0.01011238232405801\,r\right)}{5} , \sin \left(0.002297373572865413  \,r\right)+\frac{\sin \left(0.004594747145730826\,r\right)}{2}+  \frac{\sin \left(0.00689212071859624\,r\right)}{3}+\frac{\sin \left(  0.009189494291461653\,r\right)}{4}+\frac{\sin \left(  0.01148686786432707\,r\right)}{5} , \sin \left(0.002596040745477063  \,r\right)+\frac{\sin \left(0.005192081490954126\,r\right)}{2}+  \frac{\sin \left(0.007788122236431189\,r\right)}{3}+\frac{\sin   \left(0.01038416298190825\,r\right)}{4}+\frac{\sin \left(  0.01298020372738531\,r\right)}{5} , \sin \left(0.002919448107844891  \,r\right)+\frac{\sin \left(0.005838896215689782\,r\right)}{2}+  \frac{\sin \left(0.008758344323534673\,r\right)}{3}+\frac{\sin   \left(0.01167779243137956\,r\right)}{4}+\frac{\sin \left(  0.01459724053922445\,r\right)}{5} , \sin \left(0.003268563311168871  \,r\right)+\frac{\sin \left(0.006537126622337741\,r\right)}{2}+  \frac{\sin \left(0.009805689933506612\,r\right)}{3}+\frac{\sin   \left(0.01307425324467548\,r\right)}{4}+\frac{\sin \left(  0.01634281655584435\,r\right)}{5} , \sin \left(0.003644351435886262  \,r\right)+\frac{\sin \left(0.007288702871772523\,r\right)}{2}+  \frac{\sin \left(0.01093305430765878\,r\right)}{3}+\frac{\sin \left(  0.01457740574354505\,r\right)}{4}+\frac{\sin \left(  0.01822175717943131\,r\right)}{5} , \sin \left(0.004047774895164447  \,r\right)+\frac{\sin \left(0.008095549790328893\,r\right)}{2}+  \frac{\sin \left(0.01214332468549334\,r\right)}{3}+\frac{\sin \left(  0.01619109958065779\,r\right)}{4}+\frac{\sin \left(  0.02023887447582223\,r\right)}{5} , \sin \left(0.004479793338660443  \,r\right)+\frac{\sin \left(0.008959586677320885\,r\right)}{2}+  \frac{\sin \left(0.01343938001598133\,r\right)}{3}+\frac{\sin \left(  0.01791917335464177\,r\right)}{4}+\frac{\sin \left(  0.02239896669330221\,r\right)}{5} , \sin \left(0.0049413635565565\,r  \right)+\frac{\sin \left(0.009882727113112999\,r\right)}{2}+\frac{  \sin \left(0.0148240906696695\,r\right)}{3}+\frac{\sin \left(  0.019765454226226\,r\right)}{4}+\frac{\sin \left(0.0247068177827825  \,r\right)}{5} , \sin \left(0.005433439383882244\,r\right)+\frac{  \sin \left(0.01086687876776449\,r\right)}{2}+\frac{\sin \left(  0.01630031815164673\,r\right)}{3}+\frac{\sin \left(  0.02173375753552897\,r\right)}{4}+\frac{\sin \left(  0.02716719691941122\,r\right)}{5} , \sin \left(0.005956971605131645  \,r\right)+\frac{\sin \left(0.01191394321026329\,r\right)}{2}+\frac{  \sin \left(0.01787091481539493\,r\right)}{3}+\frac{\sin \left(  0.02382788642052658\,r\right)}{4}+\frac{\sin \left(  0.02978485802565822\,r\right)}{5} , \sin \left(0.006512907859185624  \,r\right)+\frac{\sin \left(0.01302581571837125\,r\right)}{2}+\frac{  \sin \left(0.01953872357755687\,r\right)}{3}+\frac{\sin \left(  0.0260516314367425\,r\right)}{4}+\frac{\sin \left(  0.03256453929592812\,r\right)}{5} , \sin \left(0.007102192544548636  \,r\right)+\frac{\sin \left(0.01420438508909727\,r\right)}{2}+\frac{  \sin \left(0.02130657763364591\,r\right)}{3}+\frac{\sin \left(  0.02840877017819454\,r\right)}{4}+\frac{\sin \left(  0.03551096272274318\,r\right)}{5} , \sin \left(0.007725766724910044  \,r\right)+\frac{\sin \left(0.01545153344982009\,r\right)}{2}+\frac{  \sin \left(0.02317730017473013\,r\right)}{3}+\frac{\sin \left(  0.03090306689964017\,r\right)}{4}+\frac{\sin \left(  0.03862883362455022\,r\right)}{5} , \sin \left(0.00838456803503801\,  r\right)+\frac{\sin \left(0.01676913607007602\,r\right)}{2}+\frac{  \sin \left(0.02515370410511403\,r\right)}{3}+\frac{\sin \left(  0.03353827214015204\,r\right)}{4}+\frac{\sin \left(  0.04192284017519005\,r\right)}{5} , \sin \left(0.009079530587017326  \,r\right)+\frac{\sin \left(0.01815906117403465\,r\right)}{2}+\frac{  \sin \left(0.02723859176105198\,r\right)}{3}+\frac{\sin \left(  0.0363181223480693\,r\right)}{4}+\frac{\sin \left(  0.04539765293508663\,r\right)}{5} , \sin \left(0.009811584876838586  \,r\right)+\frac{\sin \left(0.01962316975367717\,r\right)}{2}+\frac{  \sin \left(0.02943475463051576\,r\right)}{3}+\frac{\sin \left(  0.03924633950735434\,r\right)}{4}+\frac{\sin \left(  0.04905792438419293\,r\right)}{5} , \sin \left(0.0105816576913495\,r  \right)+\frac{\sin \left(0.021163315382699\,r\right)}{2}+\frac{\sin   \left(0.0317449730740485\,r\right)}{3}+\frac{\sin \left(  0.042326630765398\,r\right)}{4}+\frac{\sin \left(0.0529082884567475  \,r\right)}{5} , \sin \left(0.01139067201557714\,r\right)+\frac{  \sin \left(0.02278134403115428\,r\right)}{2}+\frac{\sin \left(  0.03417201604673142\,r\right)}{3}+\frac{\sin \left(  0.04556268806230857\,r\right)}{4}+\frac{\sin \left(  0.05695336007788571\,r\right)}{5} , \sin \left(0.01223954694042984\,  r\right)+\frac{\sin \left(0.02447909388085967\,r\right)}{2}+\frac{  \sin \left(0.03671864082128951\,r\right)}{3}+\frac{\sin \left(  0.04895818776171934\,r\right)}{4}+\frac{\sin \left(  0.06119773470214918\,r\right)}{5} , \sin \left(0.01312919757078923\,  r\right)+\frac{\sin \left(0.02625839514157846\,r\right)}{2}+\frac{  \sin \left(0.03938759271236769\,r\right)}{3}+\frac{\sin \left(  0.05251679028315692\,r\right)}{4}+\frac{\sin \left(  0.06564598785394615\,r\right)}{5} , \sin \left(0.01406053493400045\,  r\right)+\frac{\sin \left(0.02812106986800089\,r\right)}{2}+\frac{  \sin \left(0.04218160480200134\,r\right)}{3}+\frac{\sin \left(  0.05624213973600178\,r\right)}{4}+\frac{\sin \left(  0.07030267467000223\,r\right)}{5} , \sin \left(0.01503446588876983\,  r\right)+\frac{\sin \left(0.03006893177753966\,r\right)}{2}+\frac{  \sin \left(0.0451033976663095\,r\right)}{3}+\frac{\sin \left(  0.06013786355507933\,r\right)}{4}+\frac{\sin \left(  0.07517232944384916\,r\right)}{5} , \sin \left(0.01605189303448024\,  r\right)+\frac{\sin \left(0.03210378606896047\,r\right)}{2}+\frac{  \sin \left(0.04815567910344071\,r\right)}{3}+\frac{\sin \left(  0.06420757213792094\,r\right)}{4}+\frac{\sin \left(  0.08025946517240118\,r\right)}{5} , \sin \left(0.01711371462093175\,  r\right)+\frac{\sin \left(0.03422742924186351\,r\right)}{2}+\frac{  \sin \left(0.05134114386279526\,r\right)}{3}+\frac{\sin \left(  0.06845485848372701\,r\right)}{4}+\frac{\sin \left(  0.08556857310465876\,r\right)}{5} , \sin \left(0.01822082445851714\,  r\right)+\frac{\sin \left(0.03644164891703428\,r\right)}{2}+\frac{  \sin \left(0.05466247337555141\,r\right)}{3}+\frac{\sin \left(  0.07288329783406855\,r\right)}{4}+\frac{\sin \left(  0.09110412229258569\,r\right)}{5} , \sin \left(0.01937411182884202\,  r\right)+\frac{\sin \left(0.03874822365768404\,r\right)}{2}+\frac{  \sin \left(0.05812233548652607\,r\right)}{3}+\frac{\sin \left(  0.07749644731536809\,r\right)}{4}+\frac{\sin \left(  0.09687055914421011\,r\right)}{5} , \sin \left(0.02057446139579705\,  r\right)+\frac{\sin \left(0.0411489227915941\,r\right)}{2}+\frac{  \sin \left(0.06172338418739115\,r\right)}{3}+\frac{\sin \left(  0.0822978455831882\,r\right)}{4}+\frac{\sin \left(0.1028723069789853  \,r\right)}{5} , \sin \left(0.02182275311709253\,r\right)+\frac{  \sin \left(0.04364550623418506\,r\right)}{2}+\frac{\sin \left(  0.06546825935127759\,r\right)}{3}+\frac{\sin \left(  0.08729101246837012\,r\right)}{4}+\frac{\sin \left(  0.1091137655854627\,r\right)}{5} , \sin \left(0.02311986215626333\,r  \right)+\frac{\sin \left(0.04623972431252665\,r\right)}{2}+\frac{  \sin \left(0.06935958646878998\,r\right)}{3}+\frac{\sin \left(  0.0924794486250533\,r\right)}{4}+\frac{\sin \left(0.1155993107813166  \,r\right)}{5} , \sin \left(0.02446665879515308\,r\right)+\frac{  \sin \left(0.04893331759030617\,r\right)}{2}+\frac{\sin \left(  0.07339997638545925\,r\right)}{3}+\frac{\sin \left(  0.09786663518061234\,r\right)}{4}+\frac{\sin \left(  0.1223332939757654\,r\right)}{5} , \sin \left(0.02586400834688696\,r  \right)+\frac{\sin \left(0.05172801669377391\,r\right)}{2}+\frac{  \sin \left(0.07759202504066087\,r\right)}{3}+\frac{\sin \left(  0.1034560333875478\,r\right)}{4}+\frac{\sin \left(0.1293200417344348  \,r\right)}{5} , \sin \left(0.02731277106934082\,r\right)+\frac{  \sin \left(0.05462554213868165\,r\right)}{2}+\frac{\sin \left(  0.08193831320802247\,r\right)}{3}+\frac{\sin \left(  0.1092510842773633\,r\right)}{4}+\frac{\sin \left(0.1365638553467041  \,r\right)}{5} , \sin \left(0.02881380207911666\,r\right)+\frac{  \sin \left(0.05762760415823331\,r\right)}{2}+\frac{\sin \left(  0.08644140623734997\,r\right)}{3}+\frac{\sin \left(  0.1152552083164666\,r\right)}{4}+\frac{\sin \left(0.1440690103955833  \,r\right)}{5} , \sin \left(0.03036795126603076\,r\right)+\frac{  \sin \left(0.06073590253206151\,r\right)}{2}+\frac{\sin \left(  0.09110385379809227\,r\right)}{3}+\frac{\sin \left(0.121471805064123  \,r\right)}{4}+\frac{\sin \left(0.1518397563301538\,r\right)}{5} ,   \sin \left(0.03197606320812652\,r\right)+\frac{\sin \left(  0.06395212641625303\,r\right)}{2}+\frac{\sin \left(  0.09592818962437955\,r\right)}{3}+\frac{\sin \left(  0.1279042528325061\,r\right)}{4}+\frac{\sin \left(0.1598803160406326  \,r\right)}{5} , \sin \left(0.0336389770872163\,r\right)+\frac{\sin   \left(0.06727795417443261\,r\right)}{2}+\frac{\sin \left(  0.1009169312616489\,r\right)}{3}+\frac{\sin \left(0.1345559083488652  \,r\right)}{4}+\frac{\sin \left(0.1681948854360815\,r\right)}{5} ,   \sin \left(0.03535752660496472\,r\right)+\frac{\sin \left(  0.07071505320992943\,r\right)}{2}+\frac{\sin \left(  0.1060725798148942\,r\right)}{3}+\frac{\sin \left(0.1414301064198589  \,r\right)}{4}+\frac{\sin \left(0.1767876330248236\,r\right)}{5} ,   \sin \left(0.03713253989951881\,r\right)+\frac{\sin \left(  0.07426507979903763\,r\right)}{2}+\frac{\sin \left(  0.1113976196985564\,r\right)}{3}+\frac{\sin \left(0.1485301595980753  \,r\right)}{4}+\frac{\sin \left(0.1856626994975941\,r\right)}{5} ,   \sin \left(0.03896483946269502\,r\right)+\frac{\sin \left(  0.07792967892539004\,r\right)}{2}+\frac{\sin \left(  0.1168945183880851\,r\right)}{3}+\frac{\sin \left(0.1558593578507801  \,r\right)}{4}+\frac{\sin \left(0.1948241973134751\,r\right)}{5} ,   \sin \left(0.0408552420577305\,r\right)+\frac{\sin \left(  0.081710484115461\,r\right)}{2}+\frac{\sin \left(0.1225657261731915  \,r\right)}{3}+\frac{\sin \left(0.163420968230922\,r\right)}{4}+  \frac{\sin \left(0.2042762102886525\,r\right)}{5} , \sin \left(  0.04280455863760801\,r\right)+\frac{\sin \left(0.08560911727521603\,  r\right)}{2}+\frac{\sin \left(0.128413675912824\,r\right)}{3}+\frac{  \sin \left(0.1712182345504321\,r\right)}{4}+\frac{\sin \left(  0.2140227931880401\,r\right)}{5} , \sin \left(0.04481359426396048\,r  \right)+\frac{\sin \left(0.08962718852792095\,r\right)}{2}+\frac{  \sin \left(0.1344407827918814\,r\right)}{3}+\frac{\sin \left(  0.1792543770558419\,r\right)}{4}+\frac{\sin \left(0.2240679713198024  \,r\right)}{5} , \sin \left(0.04688314802656623\,r\right)+\frac{  \sin \left(0.09376629605313247\,r\right)}{2}+\frac{\sin \left(  0.1406494440796987\,r\right)}{3}+\frac{\sin \left(0.1875325921062649  \,r\right)}{4}+\frac{\sin \left(0.2344157401328312\,r\right)}{5} ,   \sin \left(0.04901401296344043\,r\right)+\frac{\sin \left(  0.09802802592688087\,r\right)}{2}+\frac{\sin \left(  0.1470420388903213\,r\right)}{3}+\frac{\sin \left(0.1960560518537617  \,r\right)}{4}+\frac{\sin \left(0.2450700648172022\,r\right)}{5} ,   \sin \left(0.05120697598153157\,r\right)+\frac{\sin \left(  0.1024139519630631\,r\right)}{2}+\frac{\sin \left(0.1536209279445947  \,r\right)}{3}+\frac{\sin \left(0.2048279039261263\,r\right)}{4}+  \frac{\sin \left(0.2560348799076578\,r\right)}{5} , \sin \left(  0.05346281777803219\,r\right)+\frac{\sin \left(0.1069256355560644\,r  \right)}{2}+\frac{\sin \left(0.1603884533340966\,r\right)}{3}+\frac{  \sin \left(0.2138512711121288\,r\right)}{4}+\frac{\sin \left(  0.267314088890161\,r\right)}{5} , \sin \left(0.05578231276230905\,r  \right)+\frac{\sin \left(0.1115646255246181\,r\right)}{2}+\frac{  \sin \left(0.1673469382869271\,r\right)}{3}+\frac{\sin \left(  0.2231292510492362\,r\right)}{4}+\frac{\sin \left(0.2789115638115452  \,r\right)}{5} , \sin \left(0.05816622897846346\,r\right)+\frac{  \sin \left(0.1163324579569269\,r\right)}{2}+\frac{\sin \left(  0.1744986869353904\,r\right)}{3}+\frac{\sin \left(0.2326649159138539  \,r\right)}{4}+\frac{\sin \left(0.2908311448923173\,r\right)}{5} ,   \sin \left(0.06061532802852698\,r\right)+\frac{\sin \left(  0.121230656057054\,r\right)}{2}+\frac{\sin \left(0.1818459840855809  \,r\right)}{3}+\frac{\sin \left(0.2424613121141079\,r\right)}{4}+  \frac{\sin \left(0.3030766401426349\,r\right)}{5} , \sin \left(  0.0631303649963022\,r\right)+\frac{\sin \left(0.1262607299926044\,r  \right)}{2}+\frac{\sin \left(0.1893910949889066\,r\right)}{3}+\frac{  \sin \left(0.2525214599852088\,r\right)}{4}+\frac{\sin \left(  0.315651824981511\,r\right)}{5} , \sin \left(0.06571208837185505\,r  \right)+\frac{\sin \left(0.1314241767437101\,r\right)}{2}+\frac{  \sin \left(0.1971362651155651\,r\right)}{3}+\frac{\sin \left(  0.2628483534874202\,r\right)}{4}+\frac{\sin \left(0.3285604418592752  \,r\right)}{5} , \sin \left(0.06836123997666599\,r\right)+\frac{  \sin \left(0.136722479953332\,r\right)}{2}+\frac{\sin \left(  0.205083719929998\,r\right)}{3}+\frac{\sin \left(0.273444959906664\,  r\right)}{4}+\frac{\sin \left(0.3418061998833299\,r\right)}{5} ,   \sin \left(0.07107855488944881\,r\right)+\frac{\sin \left(  0.1421571097788976\,r\right)}{2}+\frac{\sin \left(0.2132356646683464  \,r\right)}{3}+\frac{\sin \left(0.2843142195577952\,r\right)}{4}+  \frac{\sin \left(0.355392774447244\,r\right)}{5} , \sin \left(  0.07386476137264342\,r\right)+\frac{\sin \left(0.1477295227452868\,r  \right)}{2}+\frac{\sin \left(0.2215942841179303\,r\right)}{3}+\frac{  \sin \left(0.2954590454905737\,r\right)}{4}+\frac{\sin \left(  0.3693238068632171\,r\right)}{5} , \sin \left(0.07672058079958999\,r  \right)+\frac{\sin \left(0.15344116159918\,r\right)}{2}+\frac{\sin   \left(0.23016174239877\,r\right)}{3}+\frac{\sin \left(  0.30688232319836\,r\right)}{4}+\frac{\sin \left(0.3836029039979499\,  r\right)}{5} , \sin \left(0.07964672758239233\,r\right)+\frac{\sin   \left(0.1592934551647847\,r\right)}{2}+\frac{\sin \left(  0.238940182747177\,r\right)}{3}+\frac{\sin \left(0.3185869103295693  \,r\right)}{4}+\frac{\sin \left(0.3982336379119616\,r\right)}{5} ,   \sin \left(0.08264390910047736\,r\right)+\frac{\sin \left(  0.1652878182009547\,r\right)}{2}+\frac{\sin \left(0.2479317273014321  \,r\right)}{3}+\frac{\sin \left(0.3305756364019095\,r\right)}{4}+  \frac{\sin \left(0.4132195455023868\,r\right)}{5} , \sin \left(  0.0857128256298576\,r\right)+\frac{\sin \left(0.1714256512597152\,r  \right)}{2}+\frac{\sin \left(0.2571384768895728\,r\right)}{3}+\frac{  \sin \left(0.3428513025194304\,r\right)}{4}+\frac{\sin \left(  0.428564128149288\,r\right)}{5} , \sin \left(0.08885417027310427\,r  \right)+\frac{\sin \left(0.1777083405462085\,r\right)}{2}+\frac{  \sin \left(0.2665625108193128\,r\right)}{3}+\frac{\sin \left(  0.3554166810924171\,r\right)}{4}+\frac{\sin \left(0.4442708513655214  \,r\right)}{5} , \sin \left(0.09206862889003742\,r\right)+\frac{  \sin \left(0.1841372577800748\,r\right)}{2}+\frac{\sin \left(  0.2762058866701123\,r\right)}{3}+\frac{\sin \left(0.3682745155601497  \,r\right)}{4}+\frac{\sin \left(0.4603431444501871\,r\right)}{5} ,   \sin \left(0.09535688002914089\,r\right)+\frac{\sin \left(  0.1907137600582818\,r\right)}{2}+\frac{\sin \left(0.2860706400874227  \,r\right)}{3}+\frac{\sin \left(0.3814275201165636\,r\right)}{4}+  \frac{\sin \left(0.4767844001457044\,r\right)}{5} , \sin \left(  0.0987195948597075\,r\right)+\frac{\sin \left(0.197439189719415\,r  \right)}{2}+\frac{\sin \left(0.2961587845791225\,r\right)}{3}+\frac{  \sin \left(0.39487837943883\,r\right)}{4}+\frac{\sin \left(  0.4935979742985375\,r\right)}{5} , \sin \left(0.1021574371047232\,r  \right)+\frac{\sin \left(0.2043148742094465\,r\right)}{2}+\frac{  \sin \left(0.3064723113141697\,r\right)}{3}+\frac{\sin \left(  0.408629748418893\,r\right)}{4}+\frac{\sin \left(0.5107871855236162  \,r\right)}{5} , \sin \left(0.1056710629744951\,r\right)+\frac{\sin   \left(0.2113421259489903\,r\right)}{2}+\frac{\sin \left(  0.3170131889234854\,r\right)}{3}+\frac{\sin \left(0.4226842518979805  \,r\right)}{4}+\frac{\sin \left(0.5283553148724757\,r\right)}{5} ,   \sin \left(0.1092611211010309\,r\right)+\frac{\sin \left(  0.2185222422020618\,r\right)}{2}+\frac{\sin \left(0.3277833633030928  \,r\right)}{3}+\frac{\sin \left(0.4370444844041237\,r\right)}{4}+  \frac{\sin \left(0.5463056055051546\,r\right)}{5} , \sin \left(  0.1129282524731764\,r\right)+\frac{\sin \left(0.2258565049463528\,r  \right)}{2}+\frac{\sin \left(0.3387847574195292\,r\right)}{3}+\frac{  \sin \left(0.4517130098927056\,r\right)}{4}+\frac{\sin \left(  0.564641262365882\,r\right)}{5} , \sin \left(0.1166730903725168\,r  \right)+\frac{\sin \left(0.2333461807450337\,r\right)}{2}+\frac{  \sin \left(0.3500192711175505\,r\right)}{3}+\frac{\sin \left(  0.4666923614900673\,r\right)}{4}+\frac{\sin \left(0.5833654518625842  \,r\right)}{5} , \sin \left(0.1204962603100498\,r\right)+\frac{\sin   \left(0.2409925206200996\,r\right)}{2}+\frac{\sin \left(  0.3614887809301494\,r\right)}{3}+\frac{\sin \left(0.4819850412401991  \,r\right)}{4}+\frac{\sin \left(0.6024813015502489\,r\right)}{5} ,   \sin \left(0.1243983799636342\,r\right)+\frac{\sin \left(  0.2487967599272685\,r\right)}{2}+\frac{\sin \left(0.3731951398909027  \,r\right)}{3}+\frac{\sin \left(0.4975935198545369\,r\right)}{4}+  \frac{\sin \left(0.6219918998181712\,r\right)}{5} , \sin \left(  0.1283800591162231\,r\right)+\frac{\sin \left(0.2567601182324462\,r  \right)}{2}+\frac{\sin \left(0.3851401773486692\,r\right)}{3}+\frac{  \sin \left(0.5135202364648923\,r\right)}{4}+\frac{\sin \left(  0.6419002955811154\,r\right)}{5} , \sin \left(0.1324418995948859\,r  \right)+\frac{\sin \left(0.2648837991897719\,r\right)}{2}+\frac{  \sin \left(0.3973256987846578\,r\right)}{3}+\frac{\sin \left(  0.5297675983795438\,r\right)}{4}+\frac{\sin \left(0.6622094979744297  \,r\right)}{5} , \sin \left(0.1365844952106265\,r\right)+\frac{\sin   \left(0.2731689904212531\,r\right)}{2}+\frac{\sin \left(  0.4097534856318796\,r\right)}{3}+\frac{\sin \left(0.5463379808425062  \,r\right)}{4}+\frac{\sin \left(0.6829224760531327\,r\right)}{5} ,   \sin \left(0.140808431699002\,r\right)+\frac{\sin \left(  0.2816168633980041\,r\right)}{2}+\frac{\sin \left(0.4224252950970061  \,r\right)}{3}+\frac{\sin \left(0.5632337267960081\,r\right)}{4}+  \frac{\sin \left(0.7040421584950102\,r\right)}{5} , \sin \left(  0.1451142866615502\,r\right)+\frac{\sin \left(0.2902285733231005\,r  \right)}{2}+\frac{\sin \left(0.4353428599846507\,r\right)}{3}+\frac{  \sin \left(0.580457146646201\,r\right)}{4}+\frac{\sin \left(  0.7255714333077512\,r\right)}{5} , \sin \left(0.1495026295080298\,r  \right)+\frac{\sin \left(0.2990052590160597\,r\right)}{2}+\frac{  \sin \left(0.4485078885240895\,r\right)}{3}+\frac{\sin \left(  0.5980105180321194\,r\right)}{4}+\frac{\sin \left(0.7475131475401492  \,r\right)}{5} , \sin \left(0.1539740213994798\,r\right)+\frac{\sin   \left(0.3079480427989596\,r\right)}{2}+\frac{\sin \left(  0.4619220641984394\,r\right)}{3}+\frac{\sin \left(0.6158960855979192  \,r\right)}{4}+\frac{\sin \left(0.769870106997399\,r\right)}{5}   \right] $$Berikut adalah cara menggambar kurva


\>plot2d(&sum(sin((2\*k+1)\*x)/(2\*k+1),k,0,20),0,2pi):


    
    Maxima output too long!
    Error in:
    plot2d(&amp;sum(sin((2*k+1)*x)/(2*k+1),k,0,20),0,2pi): ...
                                              ^

Hal serupa juga dapat dilakukan dengan menggunakan matriks, misalkan kita akan menggambar
kurva


\>x=linspace(0,2pi,1000); k=1:100; y=sum(sin(k\*x')/k)'; plot2d(x,y):


![images/EMT4Kalkulus%20(1)-304.png](images/EMT4Kalkulus%20(1)-304.png)

# Tabel Fungsi

Terdapat cara menarik untuk menghasilkan barisan dengan ekspresi Maxima. Perintah
mxmtable() berguna untuk menampilkan dan menggambar barisan dan menghasilkan barisan sebagai
vektor kolom. 


Sebagai contoh berikut adalah barisan turunan ke-n x^x di x=1.


\>mxmtable("diffat(x^x,x=1,n)","n",1,8,frac=1);


    Maxima said:
    diff: second argument must be a variable; found errexp1
    #0: diffat(expr=[0,1.66665833335744e-7*r,1.33330666692022e-6*r,4.499797504338432e-6*r,1.066581336583994e-5*r,2.08307...,x=[[0,1.66665833335744e-7*r,1.33330666692022e-6*r,4.499797504338432e-6*r,1.066581336583994e-5*r,2.0830...)
     -- an error. To debug this try: debugmode(true);
    
     %mxmevtable:
        return mxm("@expr,@var=@value")();
    Try "trace errors" to inspect local variables after errors.
    mxmtable:
        y[#,1]=%mxmevtable(expr,var,x[#]);

\>$'sum(k, k, 1, n) = factor(ev(sum(k, k, 1, n),simpsum=true)) // simpsum:menghitung deret secara simbolik


$$\sum_{k=1}^{n}{k}=\frac{n\,\left(1+n\right)}{2}$$\>$'sum(1/(3^k+k), k, 0, inf) = factor(ev(sum(1/(3^k+k), k, 0, inf),simpsum=true))


Di sini masih gagal, hasilnya tidak dihitung.


\>$'sum(1/x^2, x, 1, inf)= ev(sum(1/x^2, x, 1, inf),simpsum=true) // ev: menghitung nilai ekspresi

\>$'sum((-1)^(k-1)/k, k, 1, inf) = factor(ev(sum((-1)^(x-1)/x, x, 1, inf),simpsum=true))


Di sini masih gagal, hasilnya tidak dihitung.


\>$'sum((-1)^k/(2\*k-1), k, 1, inf) = factor(ev(sum((-1)^k/(2\*k-1), k, 1, inf),simpsum=true))

\>$ev(sum(1/n!, n, 0, inf),simpsum=true)


Di sini masih gagal, hasilnya tidak dihitung, harusnya hasilnya e.


\>&assume(abs(x)<1); $'sum(a\*x^k, k, 0, inf)=ev(sum(a\*x^k, k, 0, inf),simpsum=true), &forget(abs(x)<1);


Deret geometri tak hingga, dengan asumsi rasional antara -1 dan 1.


\>$'sum(x^k/k!,k,0,inf)=ev(sum(x^k/k!,k,0,inf),simpsum=true)

\>$limit(sum(x^k/k!,k,0,n),n,inf)

\>function d(n) &= sum(1/(k^2-k),k,2,n); $'d(n)=d(n)

\>$d(10)=ev(d(10),simpsum=true)

\>$d(100)=ev(d(100),simpsum=true)


# Deret Taylor

Deret Taylor suatu fungsi f yang diferensiabel sampai tak hingga di sekitar x=a adalah:


\>$'e^x =taylor(exp(x),x,0,10) // deret Taylor e^x di sekitar x=0, sampai suku ke-11


    Maxima said:
    taylor: 0.1539740213994798*r cannot be a variable.
     -- an error. To debug this try: debugmode(true);
    
    Error in:
     $'e^x =taylor(exp(x),x,0,10) // deret Taylor e^x di sekitar x= ...
                                 ^

\>$'log(x)=taylor(log(x),x,1,10)// deret log(x) di sekitar x=1


