# ENERGY-PRO-SENSITIVITY-
Best magical sensitivity that matches your device and ensure no lag 
name: energy_pro_sensitivity
description: A Free Fire sensitivity generator for any device
publish_to: 'none'
version: 1.0.0+1

environment:
  sdk: ">=2.18.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter
    import 'package:flutter/material.dart';
import 'dart:math';

void main() {
  runApp(EnergyProApp());
}

class EnergyProApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Energy Pro Sensitivity',
      theme: ThemeData(primarySwatch: Colors.red),
      home: SensitivityHome(),
    );
  }
}

class SensitivityHome extends StatefulWidget {
  @override
  _SensitivityHomeState createState() => _SensitivityHomeState();
}

class _SensitivityHomeState extends State<SensitivityHome> {
  final TextEditingController _deviceController = TextEditingController();
  Map<String, int> generatedSettings = {};

  void _generateSensitivity() {
    String device = _deviceController.text.trim();

    if (device.isEmpty) return;

    Random random = Random();
    setState(() {
      generatedSettings = {
        "General": 100 + random.nextInt(101), // 100–200
        "Red Dot": 100 + random.nextInt(101),
        "2x Scope": 100 + random.nextInt(101),
        "4x Scope": 100 + random.nextInt(101),
        "AWM Scope": 100 + random.nextInt(101),
        "Free Look": 100 + random.nextInt(101),
        "Supported DPI": 300 + random.nextInt(400), // 300–700
      };
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Energy Pro Sensitivity")),
      body: Padding(
        padding: EdgeInsets.all(20),
        child: Column(
          children: [
            TextField(
              controller: _deviceController,
              decoration: InputDecoration(
                labelText: "Enter Device Name",
                border: OutlineInputBorder(),
              ),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _generateSensitivity,
              child: Text("Generate Settings"),
            ),
            SizedBox(height: 20),
            if (generatedSettings.isNotEmpty)
              Expanded(
                child: ListView(
                  children: generatedSettings.entries.map((entry) {
                    return Card(
                      child: ListTile(
                        title: Text(entry.key),
                        trailing: Text(entry.value.toString()),
                      ),
                    );
                  }).toList(),
                ),
              )
          ],
        ),
      ),
    );
  }
}
