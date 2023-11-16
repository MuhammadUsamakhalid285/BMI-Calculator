import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  var weightController = TextEditingController();
  var heightfeetController = TextEditingController();
  var heightinchsController = TextEditingController();
  var Result = "";
  var bgcolor = Colors.indigo.shade100;
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        title: Text("BMICALCULATORAPP"),
      ),
      body: Container(
        color: bgcolor,
        child: Center(
          child: Container(
            width: 300,
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              crossAxisAlignment: CrossAxisAlignment.center,
              children: [
                Text(
                  "BMI",
                  style: TextStyle(
                    fontSize: 35,
                    fontWeight: FontWeight.w500,
                  ),
                ),
                TextField(
                  controller: weightController,
                  keyboardType: TextInputType.number,
                  decoration: InputDecoration(
                    label: Text("Enter The weigt of body"),
                    prefixIcon: Icon(Icons.line_weight),
                  ),
                ),
                SizedBox(
                  height: 16,
                ),
                TextField(
                  controller: heightfeetController,
                  keyboardType: TextInputType.number,
                  decoration: InputDecoration(
                    label: Text("Enter The height(in feet)"),
                    prefix: Icon(Icons.height),
                  ),
                ),
                SizedBox(
                  height: 16,
                ),
                TextField(
                  controller: heightinchsController,
                  keyboardType: TextInputType.number,
                  decoration: InputDecoration(
                    label: Text("Enter The  Height(in inchs)"),
                    prefixIcon: Icon(Icons.height),
                  ),
                ),
                SizedBox(
                  height: 16,
                ),
                ElevatedButton(
                  onPressed: () {
                    var userweight = weightController.text.toString();
                    var userheightfeet = heightfeetController.text.toString();
                    var userheightinchs = heightinchsController.text.toString();
                    if (userweight != "" &&
                        userheightfeet != "" &&
                        userheightinchs != "") {
                      var wt = int.parse(userweight);
                      var hf = int.parse(userheightfeet);
                      var inh = int.parse(userheightinchs);
                      var tinch = (hf * 12) + inh;
                      var tcm = tinch * 2.54;
                      var tm = tcm / 100;
                      var bmi = wt / (tm * tm);
                      var message = "";
                      if (bmi > 25) {
                        message = "Your are OverWeight";
                         bgcolor= Colors.red;
                        
                        
                      } else if (bmi < 18) {
                        message = "Your are UnderWeight";
                        bgcolor= Colors.yellow;
                       
                      } else {
                        message = " Your are healthy";
                        bgcolor= Colors.green;
                      }

                      setState(() {
                        Result =
                            "$message \n Result of BMI :${bmi.toStringAsFixed(4)} ";
                      });
                    } else {
                      setState(() {
                        Result = "please fill the required blanks";
                      });
                    }
                  },
                  child: Text('Calculator'),
                ),
                Text(
                  Result,
                  style: TextStyle(
                    fontSize: 29,
                    fontWeight: FontWeight.w300,
                  ),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

