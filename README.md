# BeCAPTCHA-Mouse Benchmark
BeCAPTCHA-Mouse Benchmark for development of bot detection technologyes based on mouse dynamics

## INSTRUCTIONS FOR DOWNLOADING BeCAPTCHA-Mouse Benchmark
1) [Download license agreement](http://atvs.ii.uam.es/atvs/licenses/BeCAPTCHA_Mouse_Benchmark.pdf), send by email one signed and scanned copy to **atvs@uam.es** according to the instructions given in point 2.
 
 
2) Send an email to **atvs@uam.es**, as follows:

   *Subject:* **[DATABASE benchmark: BeCAPTCHA_Mouse_Benchmark]**

   Body: Your name, e-mail, telephone number, organization, postal mail, purpose for which you will use the database, time and date at which you sent the email with the signed license agreement.
 

3) Once the email copy of the license agreement has been received at ATVS, you will receive an email with a username, a password, and a time slot to download the database.
 

4) [Download the benchmark](http://atvs.ii.uam.es/atvs/intranet/BeCAPTCHA_Mouse_Benchmark), for which you will need to provide the authentication information given in step 4. After you finish the download, please notify by email to **atvs@uam.es** that you have successfully completed the transaction.
 

5) For more information, please contact: **atvs@uam.es**


## DESCRIPTION OF BeCAPTCHA-Mouse BENCHMARK
BeCAPTCHA-Mouse benchmark contains more than 10K synthetic mouse trayectories generated with two methods: 

**Method 1: Function-based Mouse Trajectory Synthesis**  
With this approach the mouse trajectories are generated according to three different trajectory shapes (linear, quadratic, and exponential) and three different velocity profiles (constant, logarithmic, and Gaussian). 
To generate a synthetic trajectory **{x, y}** with *M* points, first we define the initial point [*x<sub>1</sub>, y<sub>1</sub>*] and ending point [*x<sub>M</sub>, y<sub>M</sub>*]. Second, we select one of three velocity profiles: *i)* constant velocity, where the distance between adjacent points is constant; *ii)* logarithmic velocity, where the distances are gradually increasing (acceleration); and *iii)* Gaussian velocity, in which the distances first increase and then decrease when they get close to the end of the trajectory (acceleration and deceleration). Third, we generate a sequence **x** between *x<sub>1</sub>* and *x<sub>M</sub>* spaced according to the selected velocity profile. The **y** sequence is then generated according to the shape function. For example, for a shape defined by the quadratic function *y = ax<sup>2</sup> + bx + c*, we fit *b* and *c* for *a* fixed value of *a* by using the initial and ending points. We repeat the process fixing either *b* or *c*. The range of the parameters {*a, b, c*} explored is determined by analyzing real
mouse movements fitted to quadratic functions. Linear and exponential shapes are generated similarly.
Fig. 1 (trajectories D, E, and F) shows some examples of these mouse trajectories synthesized. That figure also shows the 3 diferent velocity profiles considered: the 3 trajectories in *E* have constant velocity, *F* shows acceleration (the distance between adjacent samples increases gradually), and *D* has initial acceleration and final deceleration. We can generate infinite mouse trajectories
with this approach by varying the parameters of each function.

![](https://github.com/BiDAlab/BeCAPTCHA-Mouse/blob/master/Fig5.png)
Figigure 1. Examples of mouse trajectories and their velocity profiles employed in this work: *A* is a real one extracted from a task of the database; *B* and *C* are synthetic trajectories generated with the GAN network; *D*, *E* and *F* are generated with the knowledge-based approach. Note that for each velocity profile (*D* = Gaussian, *E* = constant, *F* = logarithmic), we include the three knowledge-based trajectories (linear, quadratic, and exponential).

**Method 2: GAN-based Trajectories**  
For this approach we employ a GAN (Generative Adversarial Network),in which two neuronal networks, commonly named Generator and Discriminator, are trained one against the other (thus the \adversarial"). The architecture of the GAN is depicted in Fig. 2.

![](https://github.com/BiDAlab/BeCAPTCHA-Mouse/blob/master/Fig6.png)
Figure 2. The proposed architecture to train a GAN Generator of synthetic mouse trajectories.The Generator learns the human features of the mouse trajectories and generate human-like ones from Gaussian Noise.

The aim of the Generator is to fool the Discriminator by generating fake samples (mouse trajectories in this work) very similar to the real ones while the Discriminator has to predict whether the sample comes from the real set or is a fake created by the Generator. Once the
Generator is trained this way, then we can use it to synthesize mouse trajectories very similar to the human ones.
The topology employed in both Generator and Discriminator consist of two LSTM (Long Short-Term Memory) layers followed by a dense layer, very similar to a recurrent auto-encoder. The dense layer of the Discriminator is used as a classification layer to distinguish between fake and real mouse trajectories, while the Generator employs the dense layer to build synthetic mouse trajectories.
Fig. 1 shows two examples (trajectories B and C) of synthetic mouse trajectories generated with the GAN network and the comparison with a real one. We can observe high similarity between the two synthetic examples and the real one.
Human mouse patterns such us the initial acceleration and the final trajectory fine correction that we discussed before are automatically learned by the GAN network and reproduced in the synthetic trajectories generated.  
The human mouse trajectories employed to train the GAN network  were extracted from Chao *et al.* [1] database, which is comprised of more than 200K mouse trajectories acquired from 58 users who completed 300 repetitions of the task.In each repetition, the task was to click 8 buttons that appeared in the screen sequentially. This task was repeated twice in each session


#### BENCHMARK STRUCTURE
BeCAPTCHA-Mouse benchmark are composed by two main folders: *'DB_GAN'* which contains the synthetic GAN trayectories and *'DB_fcn'* that contains the function-based ones. Each folder has other two folders: *'raw'* folder which contains the raw data of the synthetic mouse trayectories in .txt files, and *'neuromotor'* folder that contains the neuromotor features (depicted in [3]) extracted from the raw files in .hws format. Both kind of files have the same name to match them easily.

#### FILES FORMAT
+ ROW 1: it just contains one entry with the number of sampled points of the handwritten character (N).

+ ROWS 2 to (N+1):

  + COLUMN 1: represents the X coordinate.

  + COLUMN 2: represents the y coordinate.

  + COLUMN 3: represents the timestamp.

  + COLUMN 4: represents the area covered by the finger.

  + COLUMNS 5, 6, and 7: represents the accelerometer information (X, Y, and Z axes).

  + COLUMNS 8, 9, and 10: represents the gyroscope information (X, Y, and Z axes).
  
However, information related to the area covered by the finger, accelerometer, and gyroscope (COLUMNS 5 to 10) might not be available in some cases depending on how old the acquisition device was.

#### FILES NOMENCLATURE
The nomenclature followed to name the files is as follows: uA_sB_CD.txt

+ A: indicates the number of the user.

+ B: indicates the number of the acquisition session [1, 2, ... , 6].

+ C: indicates the acquisition blocks:

  + num = numbers.
  
  + may = upper-case letters.
  
  + min = lower-case letters.
  
  + simb = symbols.
  
+ D: indicates the specific character/password inside each block [(0,1,.,9); (A,B,.,Z); (a,b,.,z); (?, #,.,?)]. For the case of symbols, the nomenclature is as follows:

  + _simb1 = "?" symbol.
  
  + _simb2 = "#" symbol.
  
  + _simb3 = "*" symbol.
  
  + _simb4 = "@" symbol.
  
  + _simb5 = "%" symbol.
  
  + _simb6 = "=" symbol.
  
  + _simb7 = "ε" symbol.
  
  + _simb8 = "α" symbol.
  
* Please note that there is a mistake in Fig. 2. There are 158 users with at least two sessions, not 159.

#### REFERENCES
For further information on the database and on different applications where it has been used, we refer the reader to (all these articles are publicly available in the [publications](http://atvs.ii.uam.es/atvs/listpublications.do) section of the BiDA group webpage.)

+ [TIFS2020_MobileTouchDB] R. Tolosana, R. Vera-Rodriguez, J. Fierrez and J. Ortega-Garcia, “BioTouchPass2: Touchscreen Password Biometrics Using Time-Aligned Recurrent Neural Networks”, *IEEE Transactions on Information Forensics and Security*, vol. 15, pp: 2616-2628, 2020.

+ [CVPR2019_MobileTouchDB] R. Tolosana, J. Gismero-Trujillo, R. Vera-Rodriguez, J. Fierrez and J. Ortega-Garcia, "MobileTouchDB: Mobile Touch Character Database in the Wild and Biometric Benchmark", in *Proc. IEEE Conf. on Computer Vision and Pattern Recognition Workshops, CVPRw*, Long Beach, USA, 2019.

Please remember to reference articles [CVPR2019_MobileTouchDB] on any work made public, whatever the form, based directly or indirectly on any part of the MobileTouchDB database.
