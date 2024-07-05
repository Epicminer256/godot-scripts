# godot-scripts
A collection of scripts I made. Free domain of course!

# Web export vibrate

On the top bar, goto Project > Export > Web

Put this code in the head include

```
<script>
function vibrate(id, small, large, duration){
navigator.getGamepads()[id].vibrationActuator.playEffect('dual-rumble', {
		  startDelay: 0,
		  duration: duration*1000,
		  weakMagnitude: small,
		  strongMagnitude: large,
		}).then(() => {
		  if(this.go) this.vibrate();
		})}
</script>
```

Now just insert the following function in your Godot script to vibrate the controller (when calling the function you can set the id to zero)
```
func vibrate(id, small, large, duration):
	if OS.get_name() == "Web":
		var window = JavaScriptBridge.get_interface("window")
		window.vibrate(id, small, large, duration)
	else:
		Input.start_joy_vibration(id, small, large, duration)

```
