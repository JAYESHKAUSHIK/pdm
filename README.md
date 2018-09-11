# pdm
clc;
fs=8000;
ts=1/8000;
t=0:ts:0.2;
fm1=50;fm2=100;
fc1=2000;fc2=1000;
Vm1=2;Vm2=8;
m1=Vm1/Vc1;m2=Vm2/Vc2;
y1=(1+(0.5*sin(2*pi*fm1*t)).*sin(2*pi*fc1*t));
subplot(3,3,1);
plot(t,y1);
y2=(1+(0.5*sin(2*pi*fm2*t)).*sin(2*pi*fc2*t));
subplot(3,3,2);
plot(t,y2);
y=y1+y2;
subplot(3,3,3);
plot(t,y);
d1=length(y1);
NFFT=2^nextpow2(d1);
x1=fft(y1,NFFT)/d1;
f1=fs/2*linspace(0,1,NFFT/2+1);
subplot(3,3,4);
plot(f1,2.*abs(x1(1:NFFT/2+1)));
dy1=y1.*sin(2*pi*fc1*t);
x=fft(dy1,NFFT)/d1;
f1=fs/2*linspace(0,1,NFFT/2+1);
subplot(3,3,5);
plot(f1,2*abs(x1(1:NFFT/2+1)));
h1=fir1(8,0.01);
dmod1=filter(h1,1,dy1);
subplot(3,3,6);
plot(t,dmod1);
d2=length(y2);
NFFT=2^nextpow2(d2);
x2=fft(y2,NFFT)/d2;
f2=fs/2 * linspace(0,1,NFFT/2+1);
subplot(3,3,7);
plot(f2,2*abs(x2(1:NFFT/2+1)));
dy2=y2.*sin(2*pi*fc2*t);
x2=fft(dy2,NFFT)/d2;
f2=fs/2*linspace(0,1,NFFT/2+1);
subplot(3,3,8);
plot(f2,2*abs(x2(1:NFFT/2+1)));
h2=fir1(8,0.01);
dmod2=filter(h2,1,dy2);
subplot(3,3,9);
plot(t,dmod2);
