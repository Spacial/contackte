(
s.waitForBoot {
	// Start microphone input
	{
		var micInput, reverb, delay, pitch, inverseWave;
		var mouseX, mouseY;
        var output;

		// Get the microphone input
		micInput = SoundIn.ar(0);  // Change 0 to appropriate microphone input channel if necessary

		// Get mouse positions (0 to 1)
		mouseX = MouseX.kr(0, 1);  // Controls horizontal axis
		mouseY = MouseY.kr(0, 1);  // Controls vertical axis

		// Apply effects based on mouse position

		// 1. Reverb effect (top-left corner)
		reverb = FreeVerb.ar(micInput, mix: (1 - mouseX) * mouseY, room: 0.7, damp: 0.5);

		// 2. Delay effect (top-right corner)
		delay = CombN.ar(micInput, maxdelaytime: 0.5, delaytime: mouseX * 0.5, decaytime: 1 - mouseY);

		// 3. Pitch shift effect (bottom-left corner)
		pitch = PitchShift.ar(micInput, pitchRatio: mouseY.linexp(0, 1, 0.5, 2), timeDispersion: 0.01, windowSize: 0.1);

		// 4. Inverse wave effect (bottom-right corner)
        inverseWave = micInput.neg * (1 - mouseY) * mouseX;

		// Mix effects based on mouse position

        output = reverb + delay + pitch + inverseWave;

		// Output the final signal
        Out.ar(0, output);
	}.play;
};
)
