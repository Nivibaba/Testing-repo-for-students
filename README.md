import 'package:flutter/material.dart';
import 'package:flutter_quill/flutter_quill.dart' as quill;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  late quill.QuillController _controller;
  bool _showFormattedText = false;

  @override
  void initState() {
    super.initState();
    // Initialize the controller with an empty document
    final doc = quill.Document();
    _controller = quill.QuillController(
      document: doc,
      selection: const TextSelection.collapsed(offset: 0),
    );
  }

  void _toggleFormattedText() {
    setState(() {
      _showFormattedText = !_showFormattedText;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Quill Editor Example'),
      ),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: quill.QuillToolbar.basic(controller: _controller),
          ),
          Expanded(
            child: Padding(
              padding: const EdgeInsets.all(8.0),
              child: Column(
                children: [
                  Expanded(
                    child: quill.QuillEditor(
                      controller: _controller,
                      scrollController: ScrollController(),
                      scrollable: true,
                      focusNode: FocusNode(),
                      autoFocus: true,
                      readOnly: false,
                      expands: true,
                      padding: EdgeInsets.zero,
                      customStyles: DefaultStyles(),
                    ),
                  ),
                  SizedBox(height: 20),
                  ElevatedButton(
                    onPressed: _toggleFormattedText,
                    child: Text('Show Formatted Text'),
                  ),
                  if (_showFormattedText)
                    Container(
                      padding: const EdgeInsets.all(8.0),
                      color: Colors.grey[200],
                      child: quill.QuillEditor(
                        controller: quill.QuillController(
                          document: _controller.document,
                          selection: const TextSelection.collapsed(offset: 0),
                        ),
                        scrollController: ScrollController(),
                        scrollable: true,
                        focusNode: FocusNode(),
                        autoFocus: false,
                        readOnly: true,
                        expands: false,
                        padding: EdgeInsets.zero,
                        customStyles: DefaultStyles(),
                      ),
                    ),
                ],
              ),
            ),
          ),
        ],
      ),
    );
  }
}
