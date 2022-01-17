# solar-irradiance-calculator

import math as m

# Taking Inputs

# day, month, year  = map(int, input("Enter DD:MM:YYYY ").split(":"))
# lati, tude  = map(int, input("Enter Latitude(HH.MM) ").split("."))
# longi, tude2  = map(int, input("Enter Longitude(HH.MM) ").split("."))
# std_time = float(input("Enter time in hours, HH.MM "))
# beta = float(input("Enter Collector Tilt/Slope(beta) "))
# gamma = float(input("Surface Azimuth(gamma) "))
# covers = float(input("Number of covers "))
# cover_thickness = float(input("Thickness of each glass cover(in mm) "))
# extinction = float(input("Extinction coefficient of glass(per meter) "))
# alpha = float(input("Plate Absorptivity for solar radiation  "))
# Ep = float(input("Emissivity of absorber plate "))
# K = float(input("Thermal Conductivity of Plate Material (in W/m-K) "))
# plate = float(input("Plate Thickness in mm "))
# tube = float(input("Tube centre-to-centre distance cm "))
# Outer_dia = float(input("Outer dia of tube mm "))
# Inner_dia = float(input("Inner dia of tube mm "))
# hf = float(input("Fluid to heat transfer coefficient (watt/sq meter/K) "))
# s_a = float(input("Adhesive Thickness(Enter 0 if negligible) "))
# Mass_flow_rate = float(input("Water/Mass Flow Rate (in Kg/h) "))
# absorber_length = float(input("Length of absorber plate (in meter) "))
# absorber_width = float(input("Width of absorber plate (in meter) "))
# collector_length = float(input("Length of collector (in meter) "))
# collector_width = float(input("Width of collector (in meter) "))
# Tfi = float(input("Water Inlet Temperature (in degree celcus) "))
# Ta = float(input("Ambient Temperature (in degree celcus) "))
# V_inf = float(input("Wind Speed (m/s) "))
# Ec = float(input("Emissivity of glass cover "))
# k_i = float(input("Insulation Thermal conductivity (in W/m-K) "))
# s_b_cm = float(input("Back Insulation Thickness (in cm) "))
# L_p_c = float(input("Spacing (in cm) "))






print("----------------SOLUTION--------------------")


# Test Values

day, month, year  = 15, 5, 1999
lati, tude  = 18, 32
longi, tude2  = 73, 51
std_time = 12.00
beta = 18.32
gamma = 0
covers = 2
cover_thickness = 4 
extinction = 19
alpha = 0.94
K = 350
plate = 0.15
tube = 11.3
Outer_dia = 13.7
Inner_dia = 12.5
hf = 205
s_a = 0
Mass_flow_rate = 70
absorber_length = 2
absorber_width = 0.98
collector_length = 2.08
collector_width = 1.07
Tfi = 60
Ta = 25
V_inf = 3.1
Ep = 0.14
Ec = 0.88
L_p_c = 2.5
Ib = 725
Id = 230
k_i = 0.04
s_b_cm = 5




# n value

o = month + day
k_a = 1




def n_value():
    
    
    if month == 1 :
        o = 0 + day
    elif month == 2:
        o = 31 + day
    elif month == 3:
        o = 59 + day
    elif month == 4:
        o = 90 + day
    elif month == 5:
        o = 120 + day
    elif month == 6:
        o = 151 + day
    elif month == 7:
        o = 181 +day
    elif month == 8:
        o = 212 + day
    elif month == 9:
        o = 243 + day
    elif month == 10:
        o = 273 + day
    elif month == 11:
        o = 304 + day
    elif month == 12:
        o = 334 + day
    else: print("wrong")

    return o

n = n_value()

print("The Value of n is ",n)

# delta

delta = round((23.45)*m.sin((m.pi*((360*(284+ n))/365))/180),2)
print("Declination Angle, (Delta in Degrees): ", delta)

# latitude and longitude

abc1 = float(tude/60)
Latitude_in_degree = round(int(lati) + abc1, 2)
print(f"Latitude_in_degree: {Latitude_in_degree}")

abc2 = float(tude2/60)
Longitude_in_degree = round(int(longi) + abc2, 2)
print(f"Longitude_in_degree: {Longitude_in_degree}")


# equation for correction of time 

B = ((n-1)*360)/365
# B = float(B1*3.14)/180
# print("B=", B)

ETT = (0.000075) + (0.001868*m.cos(m.radians(B)) - (0.032077*m.sin(m.radians(B))) - (0.032077*m.sin(m.radians(B))) - (0.014615*m.cos(m.radians(2*B))) - (0.04089*m.sin(m.radians(2*B))))
EED = float(ETT)
ET= float(229.18*EED)
# print("ET=", ET)

# LAT 

abc3s = float((82.50) - float(Longitude_in_degree))
abc3 = (0.06667*abc3s)

abcd4 = float(abc3) + float(ET/60)

abcd5 = (abcd4)

Lat = round((std_time -abcd5),2)

# HOUR ANGLE

hour_angle = round(float(-15*(Lat - 12)),2)
# print("hour_angle= ", hour_angle )
q = Latitude_in_degree
M = 1
k = delta
b = beta
e = gamma
w = hour_angle

# COS THETA
cos_theta = float((m.sin((q*m.pi)/180)*((m.sin((k*m.pi)/180)*m.cos((b*m.pi)/180))+(m.cos((k*m.pi)/180)*m.cos(e)*m.cos((b*m.pi)/180)*m.sin((b*m.pi)/180)))+(m.cos((q*m.pi)/180)*((m.cos((k*m.pi)/180)*m.cos((m.pi*w)/180)*m.cos((b*m.pi)/180))-(m.sin((k*m.pi)/180)*m.cos(e)*m.sin((b*m.pi)/180))))+(m.cos((k*m.pi)/180)*m.sin(e)*m.sin((m.pi*w)/180)*m.sin((b*m.pi)/180))))
theta_1 = float(m.degrees(m.acos((cos_theta))))
# 
theta = round(theta_1,2)
print(f"Angle of Incidence, Theta: {theta}")
# 
theta_s = (m.sin((q*m.pi)/180)*m.sin((k*m.pi)/180))+(m.cos((q*m.pi)/180)*m.cos((k*m.pi)/180)*m.cos((m.pi*w)/180))
# 
theta_z = (m.sin(m.radians(Latitude_in_degree))*m.sin(m.radians(delta))) + m.cos(m.radians(Latitude_in_degree))*m.cos(m.radians(delta))*m.cos(m.radians(hour_angle))


# Solar flux incident on collector, It

if n <= 21:

    A_A = 1202
    B_B = 0.141
    C_C = 0.103

elif n > 21 and n < 52:
    A_A = 1202 - (((1202 - 1187)*24)/30)
    B_B = 0.141 - (((0.141 - 0.142)*24)/30)
    C_C = 0.103 - (((0.103 - 0.104)*24)/30)

elif n == 52:
    A_A = 1202
    B_B = 0.141
    C_C = 0.103



elif n > 52 and n < 80 :
    A_A = 1187 - (((1187 - 1164)*24)/30)
    B_B = 0.142 - (((0.142 - 0.149)*24)/30)
    C_C = 0.104 - (((0.104 - 0.109)*24)/30)



elif n == 80:
    A_A = 1202
    B_B = 0.141
    C_C = 0.103




elif n > 80 and n < 101 :
    A_A = 1187 - (((1187 - 1164)*24)/30)
    B_B = 0.142 - (((0.142 - 0.149)*24)/30)
    C_C = 0.104 - (((0.104 - 0.109)*24)/30)



else:
    A_A = 1110.8
    B_B = 0.174
    C_C = 0.128

    
# print("The Value of ABC is ",A_A)

Ibnnn = B_B/m.cos(m.radians(theta_z))

Ibn = A_A*m.exp(-Ibnnn)

Ib = round(Ibn*m.cos(m.radians(theta_z)),2)
Id = round((C_C*Ib),2)

print("Ib = ",Ib)
print("Id = ",Id)

rb=((m.sin((k*m.pi)/180)*m.sin(((q-b)*m.pi)/180))+(m.cos((k*m.pi)/180)*m.cos((w*m.pi)/180)*m.cos(((q-b)*m.pi)/180)))/((m.sin((k*m.pi)/180)*m.sin((q*m.pi)/180))+(m.cos((k*m.pi)/180)*m.cos((w*m.pi)/180)*m.cos((q*m.pi)/180)))
# print(f"value of rb: {rb}")
rd=(1+m.cos((b*m.pi)/180))/2
# print(f"value of rd: {rd}")
rr=(.2*(1-m.cos((b*m.pi)/180)))/2
# print(f"value of rr: {rr}")


It = round(((Ib*rb)+(Id*rd)+(Ib+Id)*rr),2)
print(f"Solar Flux Incident on collector, It (W/sq m): {It}")
