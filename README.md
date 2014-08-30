oculus-ane
==========

* RECENT CHANGES:

We now are upgraded to 0.4.1 on the Mac side, meaning DK2 support. Yay! PC support is on the way, if anyone wants to contribute please get in touch!

Issues related to the ANE compiling incorrectly have been addressed for Mac.

*NOTE*

If you are modifying compiling the OSX ANE yourself via Xcode, be sure to change in your Preferences the Derived Data location. It should be in “Relative” mode. This way, the build.sh script will correctly find it. If there’s a simpler way to approach this, let me know. However, if all you want is the ANE you should be fine. Just look in the build directory.

Oculus ANE (Adobe Native Extension)

--- 

To connect the Oculus via the ANE, add it in the Project Properties (remember to also check it off in the ActionScript Build Packaging section!)

Connect to the Oculus in AS3:

	var _oculus:OculusANE = new OculusANE();


For every frame of your render loop, have this code:

	private function enterFrame(event:Event) : void {
		
		var quatVec:Vector.<Number> = _oculus.getCameraQuaternion();
		var quat:Quaternion = new Quaternion(-quatVec[0], -quatVec[1], quatVec[2], quatVec[3]); 
		_camera.transform = quat.toMatrix3D(_core.transform);
		_view.render();
	}

When your application is closing make sure to call the dispose method to avoid a crash by using this code:

	_oculus.dispose();