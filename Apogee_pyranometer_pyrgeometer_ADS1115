#include <Wire.h>
#include <Adafruit_ADS1015.h>
#include <math.h> 

Adafruit_ADS1115 ads1115; // shortwave sensor on diff. channel 0-1, longwave on 2-3
#define lwThermistorPin 8 //analog input pin for longwave thermistor
#define swCalibration 18.78 // sensor specific calibration for Apogee SP-510 1252
#define lwCalibrationK1 9.131 // sensor specific calibration for Apogee SL-510 1252
#define lwCalibrationK2 1.030 // sensor specific calibration for Apogee SL-510 1252
#define lwThermistorA 0.000932794 // steinhartt-Hart const. for longwave thermistor
#define lwThermistorB 0.000221451 // steinhart-Hart const. for longwave thermistor
#define lwThermistorC  0.000000126233 // steinhartt-Hart const. for longwave thermistor
#define lwThermistorVex 3.3 // excitation voltage for longwave thermistor
#define lwThermistorRbr 24900.0 // bridge resistance for longwave thermistor
#define stefBoltzConst 0.000000056704 // stefan-boltzman constant
double swRaw;
double lwRaw;
double lwTempRaw;
 
void setup()
{
  Serial.begin(250000);
  while (!Serial) { delay(1);}
  delay(2000);
  Serial.println("Setup!");
  ads1115.begin();
  ads1115.setGain(GAIN_SIXTEEN); //ADC Range: +/- 0.256V (1 bit = 0.0078125mV)
  analogReadResolution(12); // higher 12 bit ADC read on DUE
}
 
void loop()
{
  swRaw = ads1115.readADC_Differential_0_1()/128.0; // 16-bit to mV
  Serial.print("SW Raw (mV): "); Serial.print(swRaw);
  swRaw = swRaw*swCalibration; // shortwave in W/m^2
  lwRaw = ads1115.readADC_Differential_2_3()/128.0; // 16-bit to mV
  Serial.print("  LW Raw (mV): "); Serial.print(lwRaw);
  lwTempRaw = analogRead(lwThermistorPin)/1000.0; // V, real voltage
  Serial.print("  Temp Raw (V): "); Serial.print(lwTempRaw); Serial.print("      ");
  lwTempRaw = lwThermistorRbr*(lwTempRaw/(lwThermistorVex-lwTempRaw)); // thermistor resistance
  lwTempRaw = 1 / (lwThermistorA + lwThermistorB*log(lwTempRaw) + lwThermistorC*log(lwTempRaw)*log(lwTempRaw)*log(lwTempRaw)); // thermistor temp, K
  Serial.print("  Temp Real (K): "); Serial.print(lwTempRaw); Serial.print("      ");
  lwRaw = lwCalibrationK1*lwRaw + lwCalibrationK2*stefBoltzConst*lwTempRaw*lwTempRaw*lwTempRaw*lwTempRaw; // LW in W/m^2
  Serial.print("Differential shortwave: "); Serial.print(swRaw); Serial.print(" w/m^2)"); Serial.print("     ");
  Serial.print("Differential longwave: "); Serial.print(lwRaw); Serial.println(" w/m^2)");
 
  delay(1000);
}
