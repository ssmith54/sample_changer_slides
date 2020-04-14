## Indirect Sample Changer

---

@snap[north-east span-100 text-black text-10]
Indirect sample loader class initialisation
@snapend

```python
Class IndrectSampleChanger(DataProcessorAlgorithm):
	instrument_name
	number_runs
	runs
	temperature
	spectra_range
def PyInit(self):
	self.declareProperty(name='Instrument'...)
	self.declareProperty(name='Analyser'...)
	self.declareProperty(name='Reflection'...)
	self.declareProperty(name='FirstRun'...)
	self.declareProperty(name='LastRun'...)
	self.declareProperty(name='NumberSamples'...)
	self.declareProperty(name='LastRun'...)
def validateInputs(self):
	if self._run_first > self._run_last:
		print("Warning")
	if self._spectra_range[0] > self._spectra_range[1]:
		print("Another warning..")
```

@snap[south span-100 text-black text-10]
@[1-6](The class has a number of attributes which are used in the algorithm)
@[7-14](These are then initialised in an init )
@[15-19](Which is then validated through a validate inputs method.)
@snapend


---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%

@snap[east span-50 text-center]
