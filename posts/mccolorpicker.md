## [Minecraft Color Picker](<!this_page!>) {post}
###### 07/04/14 {date}



This is a color picker for Minecraft! In Minecraft, color codes are generated using a specific math formula. This does that for you! You can use it for custom leather armor colors, firework colors, etc.

If you want to know the formula for changing RGB color to Minecraft usable codes, it is blue + 256 * green + 65536 * red. Pretty simple, but hey, why do that work when this can do it for you?

<form name="color">
    <input type="color" onchange="colorFillerHex(this.form.picker.value)" name="picker">
    Hex: <input class="mcnumber" type="text" name="h" placeholder="Hex Value" onchange="colorFillerHex(this.form.h.value)" maxlength="6">
    R: <input class="mcnumber" type="number" name="r" placeholder="R" min="0" max="255" onchange="colorFillerRGB()">
    G: <input class="mcnumber" type="number" name="g" placeholder="G" min="0" max="255" onchange="colorFillerRGB()">
    B: <input class="mcnumber" type="number" name="b" placeholder="B" min="0" max="255" onchange="colorFillerRGB()">
    <br></br>
    Minecraft Color Code: <input type="text" name="output" placeholder="Pick a color!" readonly="readonly">
</form>

<script>
    function hexToR(h) {return parseInt((cutHex(h)).substring(0,2),16)}
    function hexToG(h) {return parseInt((cutHex(h)).substring(2,4),16)}
    function hexToB(h) {return parseInt((cutHex(h)).substring(4,6),16)}
    function cutHex(h) {return (h.charAt(0)=="#") ? h.substring(1,7):h}
    function componentToHex(c) {var hex = c.toString(16); return hex.length == 1 ? "0" + hex : hex;}
    function rgbToHex(r, g, b) {return "#" + componentToHex(parseInt(r)) + componentToHex(parseInt(g)) + componentToHex(parseInt(b));}
    

    
    function colorFillerRGB() {	
        red = document.color.r.value;
        green = document.color.g.value;
        blue = document.color.b.value;
        
        value = rgbToHex(red, green, blue);
        
        result(hexToR(value),hexToG(value),hexToB(value));
    }

    function colorFillerHex(value) {
        document.color.picker.value = "#" + cutHex(value);
        document.color.h.value = cutHex(value);
        document.color.picker.style.background = "#" + cutHex(value);
        
        document.color.r.value = hexToR(value);
        document.color.g.value = hexToG(value); 
        document.color.b.value = hexToB(value);
        
        result(hexToR(value),hexToG(value),hexToB(value));
    }
    
    function result(red,green,blue) {
        newCode = blue + 256 * green + 65536 * red;
        
        document.color.output.value = newCode; 
        
        return newCode;
    }
</script>
