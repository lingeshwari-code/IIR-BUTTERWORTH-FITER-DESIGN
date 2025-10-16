# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
```
clc ;
close ;
wp=input('Enter the pass band frequency (Radians )= ' );
ws=input('Enter the stop band frequency (Radians )= ' );
alphap=input( ' Enter the pass band attenuation (dB)=' );
alphas=input( ' Enter the stop band attenuation(dB)=' );
T=input('Enter the Value of sampling Time=');
//Pre warping- Bilinear Transformation 
omegap=(2/T)*tan(wp/2);
disp(omegap,'omegap=');
omegas=(2/T)*tan(ws/2);
disp(omegas,'omegas=');
//Order of the filter
N=log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap));
disp(N,'N=');
N=ceil(N);
disp(N,'Round off value of N=');
//Cut off frequency
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N)));
disp(omegac,'omegac=');
disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);
disp('Analog LPF Transfer function H(S)=');
hs= analpf(N,'butt',[0,0],omegac);
disp(hs);
z=poly(0,'z');//Defining variable z
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))
// Bilinear Transformation
disp('Digital LPF Transfer function H(Z)=');
disp(Hz);
HW=frmag(Hz,512); 
// Frequency response
w=0:%pi/511:%pi ;
plot(w/%pi,abs(HW));
xlabel(' Normalized Digital Frequency w');
ylabel('Magnitude ');
13
14
title(' Frequency Response of Butterworth IIR LPF');

```
## PROGRAM (HPF): 
```
clc;
close;

// User Inputs
wp = input('Enter the pass band frequency (Radians) = ');
ws = input('Enter the stop band frequency (Radians) = ');
alphap = input('Enter the pass band attenuation (dB) = ');
alphas = input('Enter the stop band attenuation (dB) = ');
T = input('Enter the Value of sampling Time = ');

// Prewarping using Bilinear Transformation
omegap = (2/T) * tan(wp/2);
disp(omegap, 'omegap =');
omegas = (2/T) * tan(ws/2);
disp(omegas, 'omegas =');

// Order of the filter
N = log10(((10^(0.1*alphas))-1) / ((10^(0.1*alphap))-1)) / (2*log10(omegap/omegas));
disp(N, 'N =');
N = ceil(N);
disp(N, 'Round off value of N =');

// Cutoff frequency for HPF
omegac = omegap / (( (10^(0.1*alphap)) - 1 )^(1/(2*N)));
disp(omegac, 'omegac =');

// Normalized Analog LPF Prototype
disp('Normalized Analog LPF Transfer Function H(s) =');
hs_normalised = analpf(N, 'butt', [0,0], 1);
disp(hs_normalised);

// Analog HPF Transfer function using LPF -> HPF transformation
disp('Analog HPF Transfer Function H(s) =');
hs = analpf(N, 'butt', 'high', omegac);
disp(hs);

// Bilinear Transformation to Digital Domain
z = poly(0, 'z');
Hz = horner(hs, (2/T)*((z-1)/(z+1)));
disp('Digital HPF Transfer Function H(z) =');
disp(Hz);

// Frequency Response
HW = frmag(Hz, 512);
w = 0:%pi/511:%pi;
plot(w/%pi, abs(HW));
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of Butterworth IIR High Pass Filter');

```
## OUTPUT (LPF) : 

<img width="756" height="573" alt="Screenshot 2025-09-18 135019" src="https://github.com/user-attachments/assets/8ec3d04c-b910-42ea-95aa-dd4398dd565e" />

## OUTPUT (HPF) : 
<img width="756" height="721" alt="Screenshot 2025-09-25 133741" src="https://github.com/user-attachments/assets/76327f3f-01c8-4062-94af-061e694a6cdb" />

## RESULT: 
Thus, the low pass filter and high pass filter of the butterworth  filter were performed and its result was verified.
