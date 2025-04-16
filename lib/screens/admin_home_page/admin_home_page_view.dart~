import 'package:flutter/material.dart';

class AdminHomePage extends StatefulWidget {
  const AdminHomePage({super.key});

  @override
  State<AdminHomePage> createState() => _AdminHomePageState();
}

class _AdminHomePageState extends State<AdminHomePage> {

  final List<String> technologies = ['Flutter', 'Web Dev', 'Firebase','Python','Java'];
  final List<String> levels = ['Fresher', 'Intermediate', 'Advanced'];

  String? selectedTechnology;
  String? selectedLevel;

  final Map<String, Map<String, List<Map<String, String>>>> qaDatabase = {};

  void _addQuestionDialog() {
    final TextEditingController questionController = TextEditingController();
    final TextEditingController answerController = TextEditingController();

    showDialog(
      context: context,
      builder: (_) => AlertDialog(
        title: const Text('Add Question'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              controller: questionController,
              decoration: const InputDecoration(labelText: 'Question'),
            ),
            TextField(
              controller: answerController,
              decoration: const InputDecoration(labelText: 'Answer'),
            ),
          ],
        ),
        actions: [
          TextButton(
            onPressed: () {
              if (selectedTechnology != null && selectedLevel != null) {
                final question = questionController.text.trim();
                final answer = answerController.text.trim();
                if (question.isNotEmpty && answer.isNotEmpty) {
                  setState(() {
                    qaDatabase.putIfAbsent(selectedTechnology!, () => {});
                    qaDatabase[selectedTechnology!]!
                        .putIfAbsent(selectedLevel!, () => []);
                    qaDatabase[selectedTechnology!]![selectedLevel!]!
                        .add({'question': question, 'answer': answer});
                  });
                  Navigator.pop(context);
                }
              }
            },
            child: const Text('Save'),
          ),
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    final questions = selectedTechnology != null &&
        selectedLevel != null &&
        qaDatabase[selectedTechnology!]?[selectedLevel!] != null
        ? qaDatabase[selectedTechnology!]![selectedLevel!]!
        : [];

    return Scaffold(
      appBar: AppBar(
        title: const Center(child: Text('Admin Home Page')),
      ),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          children: [
            // Technology Dropdown
            Row(
              children: [
                const Text("Select Technology: "),
                const SizedBox(width: 20),
                DropdownButton<String>(
                  value: selectedTechnology,
                  hint: const Text('Choose one'),
                  items: technologies.map((tech) =>
                      DropdownMenuItem(value: tech, child: Text(tech))).toList(),
                  onChanged: (value) {
                    setState(() {
                      selectedTechnology = value;
                      selectedLevel = null;
                    });
                  },
                ),
              ],
            ),
            const SizedBox(height: 20),
            // Level Dropdown
            if (selectedTechnology != null)
              Row(
                children: [
                  const Text("Select Level: "),
                  const SizedBox(width: 20),
                  DropdownButton<String>(
                    value: selectedLevel,
                    hint: const Text('Choose level'),
                    items: levels
                        .map((level) =>
                        DropdownMenuItem(value: level, child: Text(level)))
                        .toList(),
                    onChanged: (value) {
                      setState(() {
                        selectedLevel = value;
                      });
                    },
                  ),
                ],
              ),
            const SizedBox(height: 30),

            // Add Question Button
            if (selectedTechnology != null && selectedLevel != null)
              ElevatedButton.icon(
                onPressed: _addQuestionDialog,
                icon: const Icon(Icons.add),
                label: const Text('Add Question'),
              ),

            const SizedBox(height: 30),

            // Show Questions
            if (questions.isNotEmpty)
              Expanded(
                child: ListView.builder(
                  itemCount: questions.length,
                  itemBuilder: (_, index) {
                    final item = questions[index];
                    return Card(
                      margin: const EdgeInsets.symmetric(vertical: 8),
                      child: ListTile(
                        title: Text("Q: ${item['question']}"),
                        subtitle: Text("A: ${item['answer']}"),
                      ),
                    );
                  },
                ),
              ),
          ],
        ),
      ),
    );
  }
}
