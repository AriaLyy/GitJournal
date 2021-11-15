Dart Package for serializing ed25519 keys into the openssh format

## Usage

```dart
import 'dart:io';
import 'dart:typed_data';

import 'package:cryptography/cryptography.dart';
import 'package:openssh_ed25519/openssh_ed25519.dart';

Future<void> main() async {
  final keyPair = await Ed25519().newKeyPair();

  var privateBytes = Uint8List.fromList(await keyPair.extractPrivateKeyBytes());
  var public = await keyPair.extractPublicKey();
  var publicBytes = Uint8List.fromList(public.bytes);

  var publicStr = encodeEd25519Public(publicBytes);
  var privateStr = encodeEd25519Private(
    privateBytes: privateBytes,
    publicBytes: publicBytes,
  );

  await File('id_ed25519.pub').writeAsString(publicStr);
  await File('id_ed25519').writeAsString(privateStr);
}

```