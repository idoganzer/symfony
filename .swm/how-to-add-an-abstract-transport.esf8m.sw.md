---
id: esf8m
name: How to Add an Abstract Transport
file_version: 1.0.2
app_version: 0.7.10-0
file_blobs:
  src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatTransportFactory.php: ae74ee689b9afc1110fabbd2bf8853eafa598105
  src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php: c7dd020a7eb9a33cef929534fbb64ee40be03755
  src/Symfony/Component/Notifier/Transport/AbstractTransport.php: 7c73c5b3f5f7ba330cc10cb58a68a9927e230400
  src/Symfony/Component/Notifier/Bridge/TurboSms/TurboSmsTransport.php: c48d0df4a53741033adc64ca03c927cbe53f815c
  src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatEmailTransport.php: 6728716b1adf2f1666833bc36dc54d55e137eb61
  src/Symfony/Component/Notifier/Bridge/AmazonSns/AmazonSnsTransport.php: 810ff8c310d3be80bec76f45fc8c5bde6bed4ea4
  src/Symfony/Component/Notifier/Bridge/FakeSms/FakeSmsEmailTransport.php: 1c4c883e02774396e7d9489e965f6d068607f50e
---

This document covers how to create a new Abstract Transport.

An Abstract Transport is {Explain what a Abstract Transport is and its role in the system}

Some examples of `AbstractTransport`[<sup id="1oY7QH">↓</sup>](#f-1oY7QH)s are `TurboSmsTransport`[<sup id="cib7j">↓</sup>](#f-cib7j), `FakeChatEmailTransport`[<sup id="Z1zulf2">↓</sup>](#f-Z1zulf2), `AmazonSnsTransport`[<sup id="Z2rAvva">↓</sup>](#f-Z2rAvva), and `FakeSmsEmailTransport`[<sup id="Z23YP7D">↓</sup>](#f-Z23YP7D).

<br/>

## TL;DR - How to Add a `AbstractTransport`[<sup id="1oY7QH">↓</sup>](#f-1oY7QH)

1.  Create a new class inheriting from HELLO
    
    *   Place the file in one of the directories under [[sym:././src/Symfony/Component/Notifier/Bridge({&quot;type&quot;:&quot;path&quot;,&quot;text&quot;:&quot;src/Symfony/Component/Notifier/Bridge&quot;,&quot;path&quot;:&quot;src/Symfony/Component/Notifier/Bridge&quot;})]], e.g. `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9) is defined in [[sym:././src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php({&quot;type&quot;:&quot;path&quot;,&quot;text&quot;:&quot;src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php&quot;,&quot;path&quot;:&quot;src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php&quot;})]].
        
2.  Define `HOST`[<sup id="1dbbRb">↓</sup>](#f-1dbbRb).
    
3.  Implement `__construct`[<sup id="1qpt6x">↓</sup>](#f-1qpt6x), `__toString`[<sup id="Z1nLcBg">↓</sup>](#f-Z1nLcBg), `doSend`[<sup id="14PCqW">↓</sup>](#f-14PCqW), and `supports`[<sup id="Z26YdGT">↓</sup>](#f-Z26YdGT).
    
4.  **Profit** 💰

<br/>

## The Full Story
We'll follow the implementation of `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9) for this example.

A `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9) is {Explain what FakeChatLoggerTransport is and how it works with the Abstract Transport interface}

<br/>

### `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9) Usage Example
For example, this is how `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9) can be used:
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatTransportFactory.php
```hack
⬜ 47             }
⬜ 48     
⬜ 49             if ('fakechat+logger' === $scheme) {
🟩 50                 return new FakeChatLoggerTransport($this->logger);
⬜ 51             }
⬜ 52     
⬜ 53             throw new UnsupportedSchemeException($dsn, 'fakechat', $this->getSupportedSchemes());
```

<br/>

## Steps to Adding a new AbstractTransport

<br/>

### 1\. Inherit from `AbstractTransport`[<sup id="1oY7QH">↓</sup>](#f-1oY7QH).
All `AbstractTransport`[<sup id="1oY7QH">↓</sup>](#f-1oY7QH)s are defined under [[sym:./src/Symfony/Component/Notifier/Bridge({"type":"path","text":"src/Symfony/Component/Notifier/Bridge","path":"src/Symfony/Component/Notifier/Bridge"})]].

<br/>

We first need to define our class in the relevant file, and inherit from `AbstractTransport`[<sup id="1oY7QH">↓</sup>](#f-1oY7QH):
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php
```hack
⬜ 23     /**
⬜ 24      * @author Antoine Makdessi <amakdessi@me.com>
⬜ 25      */
🟩 26     final class FakeChatLoggerTransport extends AbstractTransport
⬜ 27     {
⬜ 28         protected const HOST = 'default';
⬜ 29     
```

<br/>

> **Note**: the class name should end with "Transport".

<br/>

### 2\. Define `HOST`[<sup id="1dbbRb">↓</sup>](#f-1dbbRb)
Every `AbstractTransport`[<sup id="1oY7QH">↓</sup>](#f-1oY7QH) should define this variable:
- `HOST`[<sup id="1dbbRb">↓</sup>](#f-1dbbRb): {Explain what the value should be}

<br/>


<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php
```hack
⬜ 25      */
⬜ 26     final class FakeChatLoggerTransport extends AbstractTransport
⬜ 27     {
🟩 28         protected const HOST = 'default';
⬜ 29     
⬜ 30         private LoggerInterface $logger;
⬜ 31     
```

<br/>

### 3\. Implement \_\_construct, \_\_toString, doSend, and supports

<br/>

The goal of `__construct`[<sup id="1qpt6x">↓</sup>](#f-1qpt6x) is to {Explain __construct's role}.

<br/>

In this example, `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9), we {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php
```hack
⬜ 29     
⬜ 30         private LoggerInterface $logger;
⬜ 31     
🟩 32         public function __construct(LoggerInterface $logger, HttpClientInterface $client = null, EventDispatcherInterface $dispatcher = null)
⬜ 33         {
⬜ 34             $this->logger = $logger;
⬜ 35     
```

<br/>

The goal of `__toString`[<sup id="Z1nLcBg">↓</sup>](#f-Z1nLcBg) is to {Explain __toString's role}.

<br/>

In this example, `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9), we {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php
```hack
⬜ 36             parent::__construct($client, $dispatcher);
⬜ 37         }
⬜ 38     
🟩 39         public function __toString(): string
⬜ 40         {
⬜ 41             return sprintf('fakechat+logger://%s', $this->getEndpoint());
⬜ 42         }
```

<br/>

The goal of `doSend`[<sup id="14PCqW">↓</sup>](#f-14PCqW) is to {Explain doSend's role}.

<br/>

In this example, `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9), we {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php
```hack
⬜ 49         /**
⬜ 50          * @param MessageInterface|ChatMessage $message
⬜ 51          */
🟩 52         protected function doSend(MessageInterface $message): SentMessage
⬜ 53         {
⬜ 54             if (!$this->supports($message)) {
⬜ 55                 throw new UnsupportedMessageTypeException(__CLASS__, ChatMessage::class, $message);
```

<br/>

The goal of `supports`[<sup id="Z26YdGT">↓</sup>](#f-Z26YdGT) is to {Explain supports's role}.

<br/>

In this example, `FakeChatLoggerTransport`[<sup id="1AmKs9">↓</sup>](#f-1AmKs9), we {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php
```hack
⬜ 41             return sprintf('fakechat+logger://%s', $this->getEndpoint());
⬜ 42         }
⬜ 43     
🟩 44         public function supports(MessageInterface $message): bool
⬜ 45         {
⬜ 46             return $message instanceof ChatMessage;
⬜ 47         }
```

<br/>

<!-- THIS IS AN AUTOGENERATED SECTION. DO NOT EDIT THIS SECTION DIRECTLY -->
### Swimm Note

<span id="f-1qpt6x">__construct</span>[^](#1qpt6x) - "src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php" L32
```hack
    public function __construct(LoggerInterface $logger, HttpClientInterface $client = null, EventDispatcherInterface $dispatcher = null)
```

<span id="f-Z1nLcBg">__toString</span>[^](#Z1nLcBg) - "src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php" L39
```hack
    public function __toString(): string
```

<span id="f-1oY7QH">AbstractTransport</span>[^](#1oY7QH) - "src/Symfony/Component/Notifier/Transport/AbstractTransport.php" L27
```hack
abstract class AbstractTransport implements TransportInterface
```

<span id="f-Z2rAvva">AmazonSnsTransport</span>[^](#Z2rAvva) - "src/Symfony/Component/Notifier/Bridge/AmazonSns/AmazonSnsTransport.php" L28
```hack
final class AmazonSnsTransport extends AbstractTransport
```

<span id="f-14PCqW">doSend</span>[^](#14PCqW) - "src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php" L52
```hack
    protected function doSend(MessageInterface $message): SentMessage
```

<span id="f-Z1zulf2">FakeChatEmailTransport</span>[^](#Z1zulf2) - "src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatEmailTransport.php" L28
```hack
final class FakeChatEmailTransport extends AbstractTransport
```

<span id="f-1AmKs9">FakeChatLoggerTransport</span>[^](#1AmKs9) - "src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php" L26
```hack
final class FakeChatLoggerTransport extends AbstractTransport
```

<span id="f-Z23YP7D">FakeSmsEmailTransport</span>[^](#Z23YP7D) - "src/Symfony/Component/Notifier/Bridge/FakeSms/FakeSmsEmailTransport.php" L29
```hack
final class FakeSmsEmailTransport extends AbstractTransport
```

<span id="f-1dbbRb">HOST</span>[^](#1dbbRb) - "src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php" L28
```hack
    protected const HOST = 'default';
```

<span id="f-Z26YdGT">supports</span>[^](#Z26YdGT) - "src/Symfony/Component/Notifier/Bridge/FakeChat/FakeChatLoggerTransport.php" L44
```hack
    public function supports(MessageInterface $message): bool
```

<span id="f-cib7j">TurboSmsTransport</span>[^](#cib7j) - "src/Symfony/Component/Notifier/Bridge/TurboSms/TurboSmsTransport.php" L29
```hack
final class TurboSmsTransport extends AbstractTransport
```

<br/>

This file was generated by Swimm. [Click here to view it in the app](http://localhost:5000/repos/Z2l0aHViJTNBJTNBc3ltZm9ueSUzQSUzQWlkb2dhbnplcg==/docs/esf8m).