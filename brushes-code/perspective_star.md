# Perspective Star

TODO: Description


## Code

```
cfg{
	name = "Perspective Star" ;
}

perPrim {	
	float numStep = 8;
	{
		uiName = "Number Steps";
		uiFormat = integer;
	}
	float thickness = 3.0;
	{
		uiName = "Thickness";
	}
}

float4 main( idatas i )
{
	float4 finalCol = float4(0, 0, 0, 0);
	int ns = ceil(i.numStep);
	float step = (2 * PI) / ns;

	// for each ray, we check that the current pixel is close enough
	// from the perfect theoretical position for the ray, given the
	// current distance from origin
	for (int j = 0; j < ns; j++) {


		float2 perfectPos = float2(cos(step * j), sin(step * j));
		perfectPos *= distance(i.pos, i.strokePos);
		perfectPos += i.strokePos;



		if (distance(i.pos, perfectPos) < i.thickness) {
			finalCol = i.color;
		}
    }

	return finalCol;
}
```