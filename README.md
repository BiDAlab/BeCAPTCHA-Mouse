# BeCAPTCHA-Mouse Benchmark
BeCAPTCHA-Mouse Benchmark for development of bot detection technologyes based on mouse dynamics

## INSTRUCTIONS FOR DOWNLOADING BeCAPTCHA-Mouse Benchmark
1) [Download license agreement](http://atvs.ii.uam.es/atvs/licenses/MobileTouchDB_License.pdf), send by email one signed and scanned copy to **atvs@uam.es** according to the instructions given in point 2.
 
 
2) Send an email to **atvs@uam.es**, as follows:

   *Subject:* **[DATABASE download: MobileTouchDB]**

   Body: Your name, e-mail, telephone number, organization, postal mail, purpose for which you will use the database, time and date at which you sent the email with the signed license agreement.
 

3) Once the email copy of the license agreement has been received at ATVS, you will receive an email with a username, a password, and a time slot to download the database.
 

4) [Download the database](http://atvs.ii.uam.es/atvs/intranet/free_DB/MobileTouchDB), for which you will need to provide the authentication information given in step 4. After you finish the download, please notify by email to **atvs@uam.es** that you have successfully completed the transaction.
 

5) For more information, please contact: **atvs@uam.es**


## DESCRIPTION OF BeCAPTCHA-Mouse BENCHMARK

BeCAPTCHA-Mouse BENCHMARK contains more than 10K synthetic mouse trayectories generated with two methods: 

**Method 1: Knowledge-based Mouse Trajectory Synthesis**

WIth this method the mouse trajectories are generated according to three different trajectory shapes (linear, quadratic, and exponential) and three different velocity profiles (constant, logarithmic, and Gaussian). 
To generate a synthetic trajectory **{x, y}** with M points, first we define the initial point ($$\hat{x}_{0}$$, $$\hat{y}_{0}$$) and ending point . Second, we select one of three velocity profiles: \textit{i)} constant velocity, where the distance between adjacent points is constant; \textit{ii)} logarithmic velocity, where the distances are gradually increasing (acceleration); and \textit{iii)} Gaussian velocity, in which the distances first increase and then decrease when they get close to the end of the trajectory (acceleration and deceleration). Third, we generate a sequence $\mathbf{\hat{x}}$ between $\hat{x}_{0}$ and $\hat{x}_{M}$ spaced according to the selected velocity profile. The $\mathbf{\hat{y}}$ sequence is then generated according to the shape function. For example, for a shape defined by the quadratic function $\mathbf{\hat{y}} = a\mathbf{\hat{x}^{2}} + b\mathbf{\hat{x}} + c$, we fit $b$ and $c$ for different values of $a$, the known $\mathbf{\hat{x}}$ sequence, and the initial and ending points. We repeat the process for $b$ and $c$.  The range of the parameters ($a$, $b$, $c$) is determined by analyzing real mouse movements fitted to quadratic functions. Linear and exponential shapes are generated similarly.


on-line character samples performed by **217 users, using 94 different smartphone models**, with an average of 314 samples per user. In each acquisition session, users had to draw all numbers (from 0 to 9), upper- and lower-case letters (54), different symbols (8), and passwords composed of 4 numbers (6). Regarding the acquisition protocol, MobileTouchDB comprises a maximum of 6 captured sessions per subject with a time gap between them of at least 2 days. **This database studies an unsupervised mobile scenario with no restrictions in terms of position, posture, and devices. Users downloaded and used the acquisition app on their own devices freely**.

Fig. 1 represents the **different interfaces designed for the acquisition**. All interfaces are composed of: i) the character/password to draw (top, middle) and two buttons "OK" (top, right) and "Cancel" (top, left) to press after drawing if the sample was good or bad respectively. If the sample was not good, then it was repeated. And ii) a rectangular area to perform the character or password.

![](http://atvs.ii.uam.es/atvs/MobileTouchDB_interfaces_todas.jpg )
Figure 1. Different interfaces designed for the acquisition app. Both portrait and landscape orientations are considered in order to analyse different user experiences while drawing.

**The acquisition protocol considered in the MobileTouchDB database is depicted in Fig. 2**. It comprises a total of 6 sessions (i.e., S1-S6) with different time gaps among them. It is important to highlight that in all sessions, the time gap refers to the minimum time between one user finishes a session and the following session is available. However, participants usually performed their corresponding sessions later on thanks to notifications sent automatically by the acquisition app to the users.

![](http://atvs.ii.uam.es/atvs/MobileTouchDB_experimental_protocol.jpg )
Figure 2: Description of the design and number of available users of the new MobileTouchDB database.

**Regarding the data acquired, each session comprises 8 different capturing blocks (i.e., from Block1 to Block8)**. In Block1, we asked users to draw all numbers (from 0 to 9). Block2 and Block3 comprise upper- and lower-case letters respectively, with a total of 27 letters each. Block4 is composed of 8 different symbols (i.e., "?", "#", "*", "@", "%", "=", "?", and "?"). It is important to remark that inside each block, characters were randomised before asking users to draw them. This way, each user performs a different character sequence in each session. From Block1 to Block4, the acquisition interface was designed as portrait to provide a better user experience (see Fig. 1, left). After finishing the first 4 blocks focused on performing one single character at a time (one sample per character), we asked users to draw passwords composed of 4 numbers (always "5 7 8 4") in different ways (6 samples in total). In Block5, users performed the password twice using a landscape orientation interface (see Fig. 1, right). We provided the users with a graphical visualization of the numbers while drawing them (i.e., visible mode). Then, in Block6, users had to repeat once the same task considered in Block5 but this time in an invisible mode, i.e., we did not provide to the users any visualization of the numbers while drawing them. The main motivation of this novel acquisition scenario is to protect us against shoulder surfing attacks, as commented in [17]. In Block 7, users had to draw each number of the password inside of each of the four available boxes (two times), considering first a visible mode (see Fig. 1, middle). Finally, in Block8 users had to repeat once the same task considered in Block7 but this time in an invisible mode. In both Block7 and Block8 the acquisition interface was kept portrait to analyse the user experience in different settings.


#### FILES FORMAT
The handwritten characters are stored in text files, where:

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
