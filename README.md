import 'package:flutter/material.dart';
import 'package:flutter_quill/flutter_quill.dart' as quill;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Quill Editor',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: QuillEditorPage(),
    );
  }
}

class QuillEditorPage extends StatefulWidget {
  @override
  _QuillEditorPageState createState() => _QuillEditorPageState();
}

class _QuillEditorPageState extends State<QuillEditorPage> {
  final quill.QuillController _controller = quill.QuillController.basic();
  final FocusNode _focusNode = FocusNode();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Quill Editor'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            Expanded(
              child: Container(
                decoration: BoxDecoration(
                  border: Border.all(color: Colors.grey),
                ),
                child: SingleChildScrollView(
                  child: IntrinsicHeight(
                    child: Column(
                      children: [
                        quill.QuillEditor(
                          controller: _controller,
                          readOnly: false, // true for view only mode
                          autoFocus: true,
                          focusNode: _focusNode,
                          scrollController: ScrollController(),
                          scrollable: false,
                          padding: EdgeInsets.all(8.0),
                          expands: false,
                        ),
                      ],
                    ),
                  ),
                ),
              ),
            ),
            SizedBox(height: 16),
            quill.QuillToolbar.basic(controller: _controller),
          ],
        ),
      ),
    );
  }
}
