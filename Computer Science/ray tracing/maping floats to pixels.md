```
void setup() {

  Serial.begin(9600);

}



void loop() {

 sensorVal = mapf(sensorVal, sensorMin, sensorMax, -15, 15);
 Serial.println(sensorVal);
 delay(50);  
  
}


   float mapf(float x, float in_min, float in_max, float out_min, float out_max) {
     float result;
     result = (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min;
     return result;
}
```

- used in miniRT
```
/*
 * map the x from the window to our world
*/
float	map_x(float x, float min, float max)
{
	return (x * (max - min) / WIDTH - max);
}

/*
 * map the y from the window to our world
*/
float	map_y(float y, float min, float max)
{
	return (y * (max - min) / HEIGTH - max);
}
```

#References
- https://forum.arduino.cc/t/floating-point-using-map-function/348113
