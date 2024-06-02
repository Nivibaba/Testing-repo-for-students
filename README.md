# Testing-repo-for-students


import 'package:flutter/material.dart';
import 'package:flutter_markdown/flutter_markdown.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Markdown Text Editor',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MarkdownTextEditor(),
    );
  }
}

class MarkdownTextEditor extends StatefulWidget {
  @override
  _MarkdownTextEditorState createState() => _MarkdownTextEditorState();
}

class _MarkdownTextEditorState extends State<MarkdownTextEditor> {
  final TextEditingController _controller = TextEditingController();

  void _toggleBold() {
    final text = _controller.text;
    final selection = _controller.selection;
    if (selection.isValid) {
      final selectedText = text.substring(selection.start, selection.end);
      final isBold = selectedText.startsWith('**') && selectedText.endsWith('**');
      final newText = isBold
          ? selectedText.substring(2, selectedText.length - 2)
          : '**$selectedText**';
      _controller.value = TextEditingValue(
        text: text.replaceRange(selection.start, selection.end, newText),
        selection: TextSelection.collapsed(offset: selection.start + newText.length),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Markdown Text Editor'),
        actions: [
          IconButton(
            icon: Icon(Icons.format_bold),
            onPressed: _toggleBold,
          ),
        ],
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              maxLines: null,
              onChanged: (text) {
                setState(() {});
              },
              decoration: InputDecoration(
                border: OutlineInputBorder(),
                hintText: 'Enter your text with markdown here',
              ),
            ),
            SizedBox(height: 16),
            Expanded(
              child: Markdown(
                data: _controller.text,
              ),
            ),
          ],
        ),











        6666666




class _MarkdownTextEditorState extends State<MarkdownTextEditor> {
  final TextEditingController _controller = TextEditingController();
  bool _isBold = false;

  void _toggleBold() {
    final text = _controller.text;
    final selection = _controller.selection;
    if (selection.isValid) {
      final selectedText = text.substring(selection.start, selection.end);
      final newText = _isBold ? selectedText.replaceAll("**", "") : "**$selectedText**";
      _isBold = !_isBold;
      _controller.value = TextEditingValue(
        text: text.replaceRange(selection.start, selection.end, newText),
        selection: TextSelection.collapsed(offset: selection.start + newText.length),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Markdown Text Editor'),
        actions: [
          IconButton(
            icon: Icon(Icons.format_bold),
            onPressed: _toggleBold,
          ),
        ],
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              maxLines: null,
              onChanged: (text) {
                setState(() {});
              },
              style: TextStyle(fontWeight: _isBold ? FontWeight.bold : FontWeight.normal), // Apply bold style dynamically
              decoration: InputDecoration(
                border: OutlineInputBorder(),
                hintText: 'Enter your text with markdown here',
              ),
            ),
            SizedBox(height: 16),
            Expanded(
              child: Markdown(
                data: _controller.text,
              ),
            ),
          ],
        ),
      ),
    );
  }
}

66666
        
      ),
    );
  }
}
