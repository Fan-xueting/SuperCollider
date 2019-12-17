s.boot;//server

s.meter;
s.plotTree;//state of localhostInputLevel??

s.reboot;
s.quit;

////////

//Demo
Env([1, 0, 1],[1, -1],[1, -1]).kr(2);

(
SynthDef.new(\kick,{
	arg freqA = 1000, freqB = 50, freqC = 1,freqDur1 = 0.01, freqDur2 = 0.2, freqC1 =1, freqC2 = (-1),
	atk = 0.01, rel =1, c1 = 1, c2 = (-12), amp = 0.8, pan = 0, out = 0;
	var sig, env, freqSweep;
	freqSweep = Env([freqA, freqB, freqC],[freqDur1, freqDur2],[freqC1, freqC2]).ar;
	env = Env([0, 1, 0],[atk, rel],[c1,c2]).kr(2);
	sig = SinOsc.ar(freqSweep, pi/2);
	sig = sig * env;
	sig = Pan2.ar(sig, pan, amp);
	Out.ar(out,sig);
}).add
)

~myClick = Synth.new(\kick,[\freqA, 550, \atk, 0.01, \rel, 1, \amp, 1]);

//Pbindef

(
~myKick = Pbind(
	\instrument, \kick,
	\dur, 0.25,//like speed, 0.5 instead, more fast
	\freqA, 550,
    \atk, 0.01,
	\rel, 1,
	\amp, 1,
	\out,0
).play
)

/*manipulate it by using its name*/

~myKick.stop;
~myKick.play;

//Due to the reason of time, just this.~~~~
