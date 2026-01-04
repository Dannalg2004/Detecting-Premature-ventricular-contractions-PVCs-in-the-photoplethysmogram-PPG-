# ***What is a PVC?***
Premature ventricular contractions (PVCs), also known as premature ventricular complexes or ventricular extrasystoles, are early ventricular contractions due to focal electrical impulses originating from the Purkinje fibers rather than the sinoatrial (SA) node [1]. Depending on their occurrence rate, their clinical relevance ranges from completely innocuous to the development of cardiomyopathy and heart failure [2, 3].
What do PVCs look like?
On the electrocardiogram (black trace), a PVC appears as a wide, often tall, and bizarre QRS complex (see Figure 1), always followed by a longer RR interval known as the “compensatory pause.” On the photoplethysmogram (blue trace), a PVC may appear as either a missing pulse (type 1 PVC) or a premature low-amplitude pulse (type 2 PVC).

<p align="center">
  <img src="https://github.com/user-attachments/files/24419503/PVC_Dectection_PPG_Fig_01.tif" width="500">
  <br>
  <strong>Figure 1.</strong> <em>The typical appearance of a premature ventricular contraction (PVC) on the electrocardiogram (ECG) and the photoplethysmogram (PPG).</em>
</p>

# ***Why is it important to detect PVCs in PPG waveforms?***
PVCs interrupt diastolic ventricular filling, thereby decreasing stroke volume and cardiac output [4]. Therefore, the corresponding arterial pulse may be too weak to be detected by photoplethysmography (PPG)-based pulse monitors, which are the most commonly owned by the general population. Pulse under-detection can falsely appear as bradycardia, triggering unnecessary healthcare provision and causing anxiety to the patient [1, 5]. Here, we provide an open-source code for detecting PVCs in PPG signals to reduce pseudo-bradycardia alarms. Initially developed for offline PVC detection, our proposed rule-based method has now been adapted to real-time operation. 

PVC types 1 and 2 were visually identified in high-quality PPG waveforms of ten selected recordings from the multiparameter intelligent monitoring in intensive care (MIMIC) database using the synchronously recorded electrocardiograms (ECG) [6]. A .docx file with manual annotations identifying the type of PVCs and the corresponding time instants at which they occur in these recordings can be downloaded from here: Formato Anotaciones CVPs_Todos (1).docx. Please remember to cite the original study [6] when using this dataset.

# ***Access the codes***
Here the link of the codes for online detection (MATLAB and Arduino).
Offline PVC detection: Before using this code [Acá colocarás el enlace de la función que lleva por nombre “Alpinista_simple_4_CVP7_opt.m”], you need to upload the PPG and ECG signals of the MIMIC recordings into the MATLAB Workspace. Use the .docx annotation file to identify the beginning and the end of every PPG segment and smooth it by applying a Savitzky-Golay finite impulse response (FIR) filter with a polynomial order of 5 and a frame length of 15. Note that fs = 125 Hz. You’ll see the results printed on MATLAB’s Command Window.
Real-time PVC detection (MATLAB): The following code can provide you with average (every 10 seconds) and instant (every heartbeat) heart rate, also detecting PVCs in real time: [Acá colocarás el enlace del código que lleva por nombre “Alpinista_simple_4_CVP7_onine.m”]. This code works in conjunction with an Arduino UNO board and a homemade PPG circuit (see Figure 2). Verify that the COM port and baud rate match those you use to configure and connect the Arduino board [Acá colocarás el enlace del código que lleva por nombre “sketch_sep22a.ino”]. You’ll see the results printed on MATLAB’s Command Window.

<p align="center">
  <img src="https://github.com/user-attachments/files/24419507/Circuito_PPG_Mejorado.tif" width="500">
  <br>
  <strong>Figure 2.</strong> <em>A two-stage PPG analog circuit (adapted from: https://embedded-lab.com/blog/introducing-easy-pulse-a-diy-photoplethysmographic-sensor-for-measuring-heart-rate/).</em>
</p>

Optimal results can be obtained when utilizing a TCRT1000 reflective optical sensor. However, you can also adapt a TCST110 optical sensor as shown in Figure 3.

<p align="center">
  <img width="738" height="396" alt="TCST110 Adaptation" src="https://github.com/user-attachments/assets/7f8758af-24e6-4950-bf67-3b03b2d71155" />
  <br>
  <strong>Figure 3.</strong> <em>Converting a TCST110 transmissive optical sensor into a PPG reflective sensor.</em>
</p>


Real-time PVC detection (Arduino): This code works in conjunction with an Arduino UNO board and a MAX30102 High-Sensitivity Pulse Oximeter and Heart Rate sensor (see Figure 4) to provide real-time detection of PVCs: [Acá colocarás el enlace del código que lleva por nombre “Alpinista_4_CVP3_MAX.ino”]. 

<p align="center">
  <img width="714" height="577" alt="Connection MAX30102 Buzzer" src="https://github.com/user-attachments/assets/921f35b2-a32d-4642-a277-f26c343dfd98" />
  <br>
  <strong>Figure 4.</strong> <em>Circuitry schematic of the real-time PVC detector. The Arduino UNO microcontroller supplies +5V to a MAX30102 reflective PPG sensor (red line). The MAX30102 sensor’s serial data (SDA) line was connected to the microcontroller’s A4 pin (green line), whereas the SCL (serial clock) pin was wired to the microcontroller’s A5 pin (blue line). Finally, the MAX30102 module’s ground (GND) pin was connected to the Arduino UNO board’s GND pin (black line).</em>
</p>


The piezoelectric buzzer wired to the 10-pin of the microcontroller delivers a 3 kHz tone with every detected PVC, as shown in the following video:



https://github.com/user-attachments/assets/612c87d3-5832-4637-a96f-ad16b39368b2

<p align="center">
  <video width="600" controls>
    <source src="https://github.com/user-attachments/assets/612c87d3-5832-4637-a96f-ad16b39368b2" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</p>


**When using this resource, please cite the associated study, which is currently under review and is available at:** [Enlace del artículo]
How to cite: [Esto te lo paso después].

# **References**
[1]	S. Tseng, G. N. Kowlgi y C. V. DeSimone, “Management of premature ventricular complexes in the outpatient setting,” Mayo Clinic Proceedings, vol. 98, no. 7, pp. 1042–1053, julio 2023, doi: https://doi.rog/10.1016/j.mayocp.2023.01.021.

[2]	J. F. Huizar, S. G. Fisher, F. V. Ramsey, K. Kaszala, A. Y. Tan, H. Moore, J. N. Koneru, J. Kron, S. K. Padala, K. A. Ellenbogen y S. N. Singh, “Outcomes of premature ventricular contraction–cardiomyopathy in the veteran population: a secondary analysis of the CHF-STAT study,” Clinical Electrophysiology, vol. 7, no. 3, pp. 380–390, 2021, doi: https://doi.org/10.1016/j.jacep.2020.08.028.

[3]	R. A. G. Winkens, P. F. Höppener, J. A. Kragten, M. P. Verburg y H. F. J. M. Crebolder, “Are premature ventricular contractions always harmless?,” The European Journal of General Practice, vol. 20, no. 2, pp. 134–138, 2014, doi: https://doi.org/10.3109/13814788.2013.859243.

[4]	D. Zheng, J. Allen y A. Murray, “Determination of aortic valve opening time and left ventricular peak filling rate from the peripheral pulse amplitude in patients with ectopic beats,” Physiological Measurement, vol. 29, no. 12, pp. 1411–1419, 2008, doi: https://doi.org/10.1088/0967-3334/29/12/005.

[5] J. G. Kovoor y A. Thiagalingam, “Smartwatch-induced cardiology referral due to pulse underdetection with premature ventricular complexes,” HeartRhythm Case Reports, vol. 7, no. 9, pp. 585–587, 2021, doi: https://doi.org/10.1016/j.hrcr.2021.05.015.

[6] L. Goldberger, L. A. Amaral, L. Glass, J. M. Hausdorff, P. C. Ivanov, R. G. Mark, T. H. Mietus, G. B. Moody, C.-K. Peng y H. E. Stanley, “PhysioBank, PhysioToolkit, and PhysioNet: components of a new research resource for complex physiologic signals,” Circulation, vol. 101, no. 23, pp. e215–e220, 2000, doi: https://doi.org/10.1161/01.CIR.101.23.e215. 












