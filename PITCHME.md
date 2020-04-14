## Indirect Sample Changer

---

@snap[north-west span-50 text-center]
### Indirect sample changer initialisation
@snapend

```python
class IndirectSampleChanger(DataProcessorAlgorithm):
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
def _setup(self):
	self._run_frist = self.getProperty('FirstRun').value
	self._run_last = self.getProperty('LastRun').value
	self._total_range = self.getProperty('TotalRange').value
	........
```

@snap[south span-100 text-black text-10]
@[1-6](The class has a number of attributes which are used in the algorithm)
@[7-14](These are then initialised in an init )
@[15-19](Which are then validated through a validate inputs method.)
@[20-24](These validated inputs are then used to setup the class attributes)
@snapend

---
@snap[north-west span-50 text-center]
### Indirect sample changer execution
@snapend

```python
def PyExec(self)
	self._setup()
	quick_run_alg = self.createChildAlgorithm("IndirectQuickRun", 0.05, 0.95)
	for num in range(self._number_samples):
		first_run = self._run_first + num
		run_numbers = [str(first_run + idx * self._number_samples) for indx in range (num_runs)]
		quick_run_alg.setProperty('inputFiles', run_numbers)
		quick_run_alg.setProperty('Analyser', self._analyser)
		quick_run_alg.setProperty('spectraRange', self._spectra_range)
		quick_run_alg.setProperty('MSDFit', self._msd_fit)
		quick_run_alg.setProperty('ElasticRange', self._elastic_range)
		.......
```
@snap[south span-100 text-black text-10]
@[1-3,zoom](Sets up a quick run algorithm \(not sure what this is?\))
@[4-5, zoom](Loops over the samples. Runs numbers are stored as: [sample1_run_1, sample2_run_1,....,sampleN_run_1)
@[6-12](Quick_run algorithm is then set up and executed)
@snapend

---
@snap[north-west span-50 text-center]
#### Summary
@snapend2

@snap[west span-150]
@ul[list-spaced-bullets text-09]
- Takes in a number of inputs pertinent to the problem (e.g num_samples)
- Runs the quick_run algorithm for each sample, using the inputs from init
- Runs are offset: runs = [sample1_run1, sample2_run1,....,sampleN_run1, sample_1_run2...]
@ulend
@snapend
