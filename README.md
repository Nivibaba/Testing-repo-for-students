# Testing-repo-for-students


import 'package:flutter/material.dart';

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
  TextEditingController _controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Markdown Text Editor'),
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
              child: SingleChildScrollView(
                child: RichText(
                  text: TextSpan(
                    children: _buildTextSpans(_controller.text),
                  ),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }

  List<TextSpan> _buildTextSpans(String text) {
    final List<TextSpan> spans = [];
    final RegExp boldPattern = RegExp(r'\*\*(.*?)\*\*');
    final RegExp italicPattern = RegExp(r'\*(.*?)\*');

    int lastMatchEnd = 0;

    for (final match in boldPattern.allMatches(text)) {
      if (match.start > lastMatchEnd) {
        spans.add(TextSpan(text: text.substring(lastMatchEnd, match.start)));
      }
      spans.add(TextSpan(
          text: match.group(1),
          style: TextStyle(fontWeight: FontWeight.bold)));
      lastMatchEnd = match.end;
    }

    String remainingText = text.substring(lastMatchEnd);
    lastMatchEnd = 0;

    for (final match in italicPattern.allMatches(remainingText)) {
      if (match.start > lastMatchEnd) {
        spans.add(TextSpan(text: remainingText.substring(lastMatchEnd, match.start)));
      }
      spans.add(TextSpan(
          text: match.group(1),
          style: TextStyle(fontStyle: FontStyle.italic)));
      lastMatchEnd = match.end;
    }

    if (lastMatchEnd < remainingText.length) {
      spans.add(TextSpan(text: remainingText.substring(lastMatchEnd)));
    }

    return spans;
  }
}
