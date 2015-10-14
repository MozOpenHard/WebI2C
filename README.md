# WebI2C
WebI2C API polyfill implementation for CHIRIMEN is 
https://github.com/browserobo/WebI2C/implementations/Gecko

Specification for this implementation is https://github.com/browserobo/WebI2C

## how to use
This implementations requires mozi2c enabled CHIRIMEN firmware

## sample code
	var port;  
	window.addEventListener('load', function (){
	  var i2cPortNumber = 0;
	  var pcaAddress = 0x40;
	  var touchDeviceAddress = 0x5a;
	  // PCA9685 and GroveTouch are instantiated at each libraries.
	  navigator.requestI2CAccess().then(function(i2cAccess){
	    return (i2cAccess.open(0));
	  }).then(function(getPort){
	    port = getPort;
	    return (PCA9685.init(port,pcaAddress));
	  }).then(function(){
	    return (GroveTouch.init(port,touchDeviceAddress));
	  }).then(function(){
	    PCA9685.setServo( 0, 45 );
	    setInterval(function(){
	      GroveTouch.read(port,touchDeviceAddress).then(ch => {
	      .......
	      .......
	    },100);
	  });
	},false);
	.......
	.......
