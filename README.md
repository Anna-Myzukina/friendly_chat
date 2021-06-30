# friendly_chat

A new Flutter project.
![img](https://github.com/Anna-Myzukina/friendly_chat/blob/main/screenschot/screen.PNG)

## Features:

[ ] The app displays text messages in real time.
[ ] Users can enter a text string message, and send it either by pressing the Return key or the Send button.
[ ]The UI runs on Android and iOS devices, as well as the web.

## Getting Started

[x] Create a Flutter app on the command line:


        $ flutter create friendly_chat
        $ cd friendly_chat
        $ dart migrate --apply-changes
        $ flutter run
        
[x] Replace all of the code in main.dart with the following:

                import 'package:flutter/material.dart';

                void main() {
                  runApp(
                    FriendlyChatApp(),
                  );
                }

                String _name = 'Anna';

                class FriendlyChatApp extends StatelessWidget {
                  const FriendlyChatApp({
                    Key? key,
                  }) : super(key: key);

                  @override
                  Widget build(BuildContext context) {
                    return MaterialApp(
                      title: 'Chat',
                      home: ChatScreen(),
                    );
                  }
                }

                class ChatMessage extends StatelessWidget {
                  //const ChatMessage({Key? key}) : super(key: key);
                  ChatMessage({required this.text, required this.animationController});
                  final String text;
                  final AnimationController animationController;

                  @override
                  Widget build(BuildContext context) {
                    return SizeTransition(
                      sizeFactor:
                          CurvedAnimation(parent: animationController, curve: Curves.easeOut),
                      axisAlignment: 0.0,
                      child: Container(
                        child: Row(
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: [
                            Container(
                              margin: const EdgeInsets.only(right: 16.0),
                              child: CircleAvatar(child: Text(_name[0])),
                            ),
                            Column(
                              crossAxisAlignment: CrossAxisAlignment.start,
                              children: [
                                Text(_name, style: Theme.of(context).textTheme.headline4),
                                Container(
                                  margin: EdgeInsets.only(top: 5.0),
                                  child: Text(text),
                                )
                              ],
                            )
                          ],
                        ),
                      ),
                    );
                  }
                }

                class ChatScreen extends StatefulWidget {
                  const ChatScreen({Key? key}) : super(key: key);

                  @override
                  _ChatScreenState createState() => _ChatScreenState();
                }

                class _ChatScreenState extends State<ChatScreen> with TickerProviderStateMixin {
                  final List<ChatMessage> _messages = [];
                  final _textController = TextEditingController();
                  final FocusNode _focusNode = FocusNode();
                  @override
                  void dispose() {
                    for (var message in _messages) {
                      message.animationController.dispose();
                    }
                    super.dispose();
                  }

                  Widget build(BuildContext context) {
                    return Scaffold(
                      appBar: AppBar(
                        title: Text('Friendly-Chat'),
                      ),
                      body: Column(
                        children: [
                          Flexible(
                            child: ListView.builder(
                              padding: EdgeInsets.all(8.0),
                              reverse: true,
                              itemBuilder: (_, int index) => _messages[index],
                              itemCount: _messages.length,
                            ),
                          ),
                          Divider(height: 1.0),
                          Container(
                            decoration: BoxDecoration(color: Theme.of(context).cardColor),
                            child: _buildTextCompser(),
                          ),
                        ],
                      ),
                    );
                  }

                  void _handleSubmitted(String text) {
                    _textController.clear();
                    ChatMessage message = ChatMessage(
                      text: text,
                      animationController: AnimationController(
                        duration: const Duration(milliseconds: 900),
                        vsync: this,
                      ),
                    );
                    setState(() {
                      _messages.insert(0, message);
                    });
                    _focusNode.requestFocus();
                    message.animationController.forward();
                  }

                  Widget _buildTextCompser() {
                    return Container(
                      margin: EdgeInsets.symmetric(horizontal: 8.0),
                      child: Row(
                        children: [
                          Flexible(
                            child: TextField(
                              controller: _textController,
                              onSubmitted: _handleSubmitted,
                              decoration: InputDecoration.collapsed(hintText: 'Send a message'),
                              focusNode: _focusNode,
                            ),
                          ),
                          IconTheme(
                            data: IconThemeData(color: Theme.of(context).accentColor),
                            child: Container(
                              margin: EdgeInsets.symmetric(horizontal: 4.0),
                              child: IconButton(
                                  icon: const Icon(Icons.send),
                                  onPressed: () => _handleSubmitted(_textController.text)),
                            ),
                          )
                        ],
                      ),
                    );
                  }
                }
                
## Show your support

- [ ] Give a ⭐️ if you like this project!

## 📝 License

* [ ] See [LICENSE.md](https://github.com/Anna-Myzukina/startup_namer/blob/main/LICENSE.md) for details.

## Authors

👤 **Author1**
* GitHub: [Anna Muzykina](https://github.com/Anna-Myzukina)
* LinkedIn: [Anna Muzykina](https://www.linkedin.com/in/anna-muzykina/)
* email: anna.muzykina83@gmail.com

