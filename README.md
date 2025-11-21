# Design-of-FIR-Filters-using-rectangular-window
#          DESIGN OF LOW PASS FIR DIGITAL FILTER 


# AIM: 
          
  To generate design of low pass FIR digital filter using SCILAB 

# APPARATUS REQUIRED: 

  PC Installed with SCILAB 

# PROGRAM 

# LOW PASS FILTER

```
clc;
clear;
close;

// FIR Low Pass Filter Design using Fourier Series Method
// with Rectangular Window

// Step 1: Input specifications
M = input("Enter the Odd Filter Length = ");      // e.g., 21
Wc = input("Enter the Digital Cutoff Frequency (in radians) = "); // e.g., 0.4*%pi

alpha = (M - 1) / 2;     // Center index

// Step 2: Compute ideal impulse response (sinc function)
for n = 1:M
    if (n == alpha + 1) then
        hd(n) = Wc / %pi;   // At center, sinc(0) = 1
    else
        hd(n) = sin(Wc * ((n - 1) - alpha)) / (((n - 1) - alpha) * %pi);
    end
end

// Step 3: Define window coefficients (Rectangular window)
for n = 1:M
    W(n) = 1;    // Rectangular window → all ones
end

// Step 4: Apply window to impulse response
h = hd .* W;
disp(h, "Filter Coefficients are:");

// Step 5: Compute Frequency Response
[hzm, fr] = frmag(h, 256);  // 256-point frequency response

// Step 6: Plot magnitude and magnitude (dB)
subplot(2,1,1);
plot(2*fr, hzm);
xlabel("Normalized Digital Frequency (×π rad/sample)");
ylabel("Magnitude");
title("Frequency Response of FIR LPF using Rectangular Window");

subplot(2,1,2);
hzm_dB = 20 * log10(hzm);
plot(2*fr, hzm_dB);
xlabel("Normalized Digital Frequency (×π rad/sample)");
ylabel("Magnitude (dB)");
title("Frequency Response of FIR LPF using Rectangular Window (in dB)");
```

# HIGH PASS FILTER
```
clc;
clear;
close;

// FIR High Pass Filter Design using Fourier Series Method
// with Rectangular Window

// Step 1: Input specifications
M = input("Enter the Odd Filter Length = ");      // e.g., 21
Wc = input("Enter the Digital Cutoff Frequency (in radians) = "); // e.g., 0.4*%pi

alpha = (M - 1) / 2;     // Center index

// Step 2: Compute ideal LPF impulse response (sinc function)
for n = 1:M
    if (n == alpha + 1) then
        hd_lp(n) = Wc / %pi;   // At center, sinc(0) = 1
    else
        hd_lp(n) = sin(Wc * ((n - 1) - alpha)) / (((n - 1) - alpha) * %pi);
    end
end

// Step 3: Spectral inversion to get HPF
for n = 1:M
    if (n == alpha + 1) then
        hd(n) = 1 - hd_lp(n);  // center tap
    else
        hd(n) = -hd_lp(n);
    end
end

// Step 4: Define window coefficients (Rectangular window)
for n = 1:M
    W(n) = 1;    // Rectangular window → all ones
end

// Step 5: Apply window to impulse response
h = hd .* W;
disp(h, "High Pass Filter Coefficients are:");

// Step 6: Compute Frequency Response
[hzm, fr] = frmag(h, 256);  // 256-point frequency response

// Step 7: Plot magnitude and magnitude (dB)
subplot(2,1,1);
plot(2*fr, hzm);
xlabel("Normalized Digital Frequency (×π rad/sample)");
ylabel("Magnitude");
title("Frequency Response of FIR HPF using Rectangular Window");

subplot(2,1,2);
hzm_dB = 20 * log10(hzm);
plot(2*fr, hzm_dB);
xlabel("Normalized Digital Frequency (×π rad/sample)");
ylabel("Magnitude (dB)");
title("Frequency Response of FIR HPF using Rectangular Window (in dB)");

```
# OUTPUT

## LOW PASS FILTER

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/477a692b-06d9-4a0f-86dd-7dcba61bf366" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/45f4d9a3-b3ba-4b93-8c46-b9539643dc6e" />
## HIGH PASS FILTER

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0d5c3df1-fd01-413d-b593-e094c39a5283" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9efd0dc7-5b36-40e6-9c14-3e3a65a308cb" />

# RESULT
```
Thus FIR low pass and high pass filter design is performed using Rectangular Window.
```
