
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Force Resolution</title>
    <style>
        .inputContainer {
            background-color: aqua;
            padding: 20px;
            text-align: center;
            width: 40%;
            margin-left: 5%;
            margin-right: 5%;
            border-radius: 10%;
        }

        .outputContainer {
            background-color: rgb(119, 0, 255);
            padding: 20px;
            text-align: center;
            width: 40%;
            margin-left: 5%;
            margin-right: 5%;
            border-radius: 10%;

        }

        h3 {
            font-size: 40px;
        }

        button {
            font-size: 25px;
            border-radius: 10px;
            background-color: chartreuse;
            cursor: pointer;
        }

        .output {
            font-size: 24px
        }
    </style>
</head>

<body>
    <div class="mainContainer" style="display: flex;">
        <div class="inputContainer">
            <h3>Input</h3>
            <label for="force" style="font-size: 25px;">Add Force (in Newton)</label><br><br>
            <input type="number" id="force" name="force" style="width: 90px; font-size: 27px;"><br><br>
            <label for="angle" style="font-size: 24px;">Input the angle for the corresponding force w.r.t x- axis (in
                Deg)</label><br><br>
            <input type="number" id="angle" name="angle" style="width: 90px; font-size: 27px;"><br>
            <p style="font-size: 25px;">"Submit after each force and the corresponding angle"</p>
            <button type="submit" onclick="perForce()">Submit</button>
            <button type="reset" onclick="restore()">Reset</button><br>
            <div class="addedForce" id="addedForce">
                <p style="font-size: 25px; font-weight: bold;">Added Inputs: <span id="addedForce"></span></p>
            </div>
        </div>
        <div class="outputContainer">
            <h3>Output</h3>
            <p class="output" id="Sfx">&sum;Fx = 0.00N</p>
            <p class="output" id="Sfy">&sum;Fy = 0.00N</p>
            <p class="output" id="resultant">Resultant = 0.00N</p>
            <p class="output" id="angleR">Resultant Angle = 0.00&deg;</p>
        </div>
    </div>
    <script>
        let fx = 0;
        let fy = 0;
        let resultant = 0;
        let angleR = 0;
        let i = 0;

        function perForce() {
            let force = document.getElementById("force").value;
            let angle = document.getElementById("angle").value;
            if (force != "") {
                if (angle != "") {
                    let addedForceContainer = document.getElementById('addedForce');
                    let radians = angle * (Math.PI / 180);
                    fx += force * Math.cos(radians);
                    i++;
                    let fAdd = document.createElement('span');
                    fAdd.className = "fAdd";
                    fAdd.style.fontSize = "20px";
                    addedForceContainer.appendChild(fAdd);
                    fAdd.innerHTML = "F" + i + " = " + force + "N" + "&nbsp;&nbsp;&nbsp; &theta;" + "<sub>" + i + "</sub>" + " = " + angle + "°" + "<br>";
                    fy += force * Math.sin(radians);
                    resultant = Math.sqrt(fx * fx + fy * fy);
                    angleR = Math.atan(fy / fx) * (180 / Math.PI);
                    document.getElementById("Sfx").textContent = "Fx = " + fx.toFixed(2) + "N";
                    document.getElementById("Sfy").textContent = "Fy = " + fy.toFixed(2) + "N";
                    document.getElementById("resultant").textContent = "Resultant = " + resultant.toFixed(2) + "N";
                    document.getElementById("angleR").textContent = "Resultant Angle = " + angleR.toFixed(2) + "°";
                    document.getElementById("force").value = "";
                    document.getElementById("angle").value = "";
                } else {
                    alert("Enter a valid Angle")
                }
            } else {
                alert("Enter the valid Force!");
            }
        }

        function restore() {
            fx = 0;
            fy = 0;
            i = 0;
            resultant = 0;
            angleR = 0;
            document.getElementById("Sfx").textContent = "Fx = " + fx.toFixed(2) + "N";
            document.getElementById("Sfy").textContent = "Fy = " + fy.toFixed(2) + "N";
            document.getElementById("resultant").textContent = "Resultant = " + resultant.toFixed(2) + "N";
            document.getElementById("angleR").textContent = "Resultant Angle = " + angleR.toFixed(2) + "°";
            document.getElementsByClassName("fAdd").innerHTML = "";
        }
    </script>
</body>

</html>
