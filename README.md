# Testing-repo-for-students


void _toggleBold() {
  final text = _controller.text;
  final selection = _controller.selection;
  if (selection.isValid && selection.start != selection.end) {
    final selectedText = text.substring(selection.start, selection.end);
    final isBold = selectedText.startsWith('**') && selectedText.endsWith('**');
    final newText = isBold ? selectedText.substring(2, selectedText.length - 2) : '**$selectedText**';
    final modifiedText = text.replaceRange(selection.start, selection.end, newText);
    _controller.value = TextEditingValue(
      text: modifiedText,
      selection: TextSelection.collapsed(offset: selection.start + newText.length),
    );
  } else {
    final cursorPosition = selection.end;
    final newText = '**${_controller.text.substring(cursorPosition)}**';
    final modifiedText = text.replaceRange(cursorPosition, cursorPosition, newText);
    _controller.value = TextEditingValue(
      text: modifiedText,
      selection: TextSelection.collapsed(offset: cursorPosition + newText.length),
    );
  }
}
