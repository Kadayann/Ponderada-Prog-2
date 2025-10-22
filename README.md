# Ponderada de Programação em sala

## Parte feita no Tinkercad

<img width="2239" height="1399" alt="image" src="https://github.com/user-attachments/assets/480fe533-3440-4d46-88e2-e323970237b4" />

link para acessar: [https://www.tinkercad.com/things/c94aZrvhLKN-copy-of-copy-of-arduino-simulator/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=zAbrRfd81mzWo5ihAPCN-U8hgxu1Ps4J_za4MlRO7NA]

## Código no Arduino

```cpp
int pinoNoRC = 0;
int valorLido = 0;
float tensaoCapacitor = 0, tensaoResistor;
unsigned long time;

void setup() {
Serial.begin(9600);
}

void loop() {
time = millis();
valorLido = analogRead(pinoNoRC);
tensaoResistor = (valorLido * 5.0 / 1023); // 5.0V / 1023 degraus = 0.0048876
tensaoCapacitor = abs(5.0 - tensaoResistor);

Serial.print(time); // imprime o conteúdo de time no Monitor Serial
Serial.print(" ");
Serial.print(tensaoResistor);
Serial.print(" ");
Serial.println(tensaoCapacitor);

delay(400);
}
```

## Gráficos com valores no Monitor Serial

<img width="600" height="400" alt="Figure_1" src="https://github.com/user-attachments/assets/8ecf51d1-271f-4ab1-a5b4-0f6d4938082e" />

<img width="600" height="400" alt="Figure_2" src="https://github.com/user-attachments/assets/03c5e885-a712-4ecd-a6fa-cf67ee81d2a9" />

<img width="700" height="400" alt="Figure_3" src="https://github.com/user-attachments/assets/73a130e6-3fc7-484f-bf7c-1a5ba96f4868" />

## Código para os Gráficos
```cpp
import matplotlib.pyplot as plt

# Dados do monitor serial 
dados = """
0 5.00 0.00
401 4.80 0.20
803 4.61 0.39
1205 4.43 0.57
1607 4.26 0.74
2010 4.09 0.91
2412 3.93 1.07
2813 3.77 1.23
3216 3.63 1.37
3618 3.48 1.52
4021 3.34 1.66
4423 3.21 1.79
4825 3.08 1.92
5227 2.97 2.03
5629 2.85 2.15
6032 2.74 2.26
6434 2.63 2.37
6836 2.52 2.48
7238 2.42 2.58
7641 2.33 2.67
8043 2.24 2.76
8445 2.15 2.85
8847 2.06 2.94
9249 1.98 3.02
9652 1.91 3.09
10054 1.83 3.17
10457 1.76 3.24
10859 1.69 3.31
11260 1.62 3.38
11663 1.56 3.44
12065 1.50 3.50
12468 1.44 3.56
12870 1.38 3.62
13273 1.32 3.68
13675 1.28 3.72
14077 1.22 3.78
"""

#  Converter texto em listas 
tempo, vC, vR = [], [], []
for linha in dados.strip().split('\n'):
    t, c, r = linha.split()
    tempo.append(float(t))
    vC.append(float(c))
    vR.append(float(r))

#  Gráfico da carga no capacitor 
plt.figure(figsize=(6, 4))
plt.plot(tempo, vC, color='blue', linewidth=2, label='Tensão no C (Vc)')
plt.title('Carga no Capacitor (C)')
plt.xlabel('Tempo (ms)')
plt.ylabel('Tensão (V)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

#  Gráfico da descarga no resistor 
plt.figure(figsize=(6, 4))
plt.plot(tempo, vR, color='red', linewidth=2, label='Tensão no R (Vr)')
plt.title('Descarga no Resistor (R)')
plt.xlabel('Tempo (ms)')
plt.ylabel('Tensão (V)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# Comparação entre os dois 
plt.figure(figsize=(7, 4))
plt.plot(tempo, vC, color='blue', linewidth=2, label='Tensão no C (Vc)')
plt.plot(tempo, vR, color='red', linewidth=2, label='Tensão no R (Vr)')
plt.title('Comparação: Carga no C e Descarga no R')
plt.xlabel('Tempo (ms)')
plt.ylabel('Tensão (V)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()
```




