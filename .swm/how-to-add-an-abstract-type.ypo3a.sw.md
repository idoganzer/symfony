---
id: ypo3a
name: How to Add an Abstract Type
file_version: 1.0.2
app_version: 0.8.1-0
file_blobs:
  src/Symfony/Component/Form/Extension/Core/CoreExtension.php: 951bf345c0c425ab551451faa11656bc8f60d2dd
  src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php: b54ea01ca132e1cc0b45c2119025c72916cdb33c
  src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php: 5eba3a291a57cecdf40b64f06d34eb973660ecc6
  src/Symfony/Bridge/Doctrine/Form/DoctrineOrmTypeGuesser.php: f2e65a7f0a8c0ca8cebbbcc382ad4ad22bd76966
  src/Symfony/Component/Form/Extension/Core/Type/DateIntervalType.php: eeb43fc64724dc6dea637198bc935c96d06f0de7
  src/Symfony/Bundle/FrameworkBundle/Resources/config/form.php: 75bfb7eb651af918feeb9a0cfb0ca84b041881ba
  src/Symfony/Component/Form/Forms.php: 020e75eff7e2cac899a825577ecfb1028708a435
  src/Symfony/Component/Form/AbstractType.php: 3325b8bc27567f552a545f1242b0d675b2594e2e
  src/Symfony/Component/Form/Extension/Core/Type/TextType.php: 4bbd89efe7a09e5b1d5b8719e6f4025ca89f1d0b
  src/Symfony/Component/Form/Extension/Core/Type/ChoiceType.php: 3980d579fa3408fe228e964e131197106bad1673
  src/Symfony/Component/Form/Extension/Core/Type/FormType.php: b2ad2062363f9044824223081ea7ee22dcf606ff
  src/Symfony/Component/Form/Extension/Core/Type/DateType.php: 1360ed450ff6e4542f14d0adc1ef13e9ee75ef39
---

This document describes what an Abstract Type is and how to create a new one.ghj

An Abstract Type is {Explain what a Abstract Type is and its role in the system}

Some examples of `AbstractType`[<sup id="98Gmc">↓</sup>](#f-98Gmc)s are `TextType`[<sup id="Zmiw25">↓</sup>](#f-Zmiw25), `ChoiceType`[<sup id="2plHN2">↓</sup>](#f-2plHN2), `FormType`[<sup id="ENskR">↓</sup>](#f-ENskR), and `DateType`[<sup id="OosCu">↓</sup>](#f-OosCu). Note: some of these examples inherit indirectly from `AbstractType`[<sup id="98Gmc">↓</sup>](#f-98Gmc).

<br/>

## TL;DR - How to Add a `AbstractType`[<sup id="98Gmc">↓</sup>](#f-98Gmc)

1. Create a new class inheriting from `AbstractType`[<sup id="98Gmc">↓</sup>](#f-98Gmc)&nbsp;
   - Place the file under [[sym:./src/Symfony/Component/Form/Extension/Core/Type({"type":"path","text":"src/Symfony/Component/Form/Extension/Core/Type","path":"src/Symfony/Component/Form/Extension/Core/Type"})]],
     e.g. `HiddenType`[<sup id="ZI92jX">↓</sup>](#f-ZI92jX) is defined in [[sym:./src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php({"type":"path","text":"src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php","path":"src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php"})]].
2. Implement `configureOptions`[<sup id="fbhew">↓</sup>](#f-fbhew) and `getBlockPrefix`[<sup id="Z1pr0ud">↓</sup>](#f-Z1pr0ud).
3. Update [[sym:./src/Symfony/Component/Form/Extension/Core/CoreExtension.php({"type":"path","text":"src/Symfony/Component/Form/Extension/Core/CoreExtension.php","path":"src/Symfony/Component/Form/Extension/Core/CoreExtension.php"})]].
4. **Profit** 💰

<br/>

## The Full Story
We'll follow the implementation of `HiddenType`[<sup id="ZI92jX">↓</sup>](#f-ZI92jX) for this example.

A `HiddenType`[<sup id="ZI92jX">↓</sup>](#f-ZI92jX) is {Explain what HiddenType is and how it works with the Abstract Type interface}

<br/>

### `HiddenType`[<sup id="ZI92jX">↓</sup>](#f-ZI92jX) Usage Example
For example, this is how `HiddenType`[<sup id="ZI92jX">↓</sup>](#f-ZI92jX) can be used:
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Extension/Core/CoreExtension.php
```hack
⬜ 52                 new Type\DateType(),
⬜ 53                 new Type\DateTimeType(),
⬜ 54                 new Type\EmailType(),
🟩 55                 new Type\HiddenType(),
⬜ 56                 new Type\IntegerType(),
⬜ 57                 new Type\LanguageType(),
⬜ 58                 new Type\LocaleType(),
```

<br/>

## Steps to Adding a new AbstractType

<br/>

### 1\. Inherit from `AbstractType`[<sup id="98Gmc">↓</sup>](#f-98Gmc).
All `AbstractType`[<sup id="98Gmc">↓</sup>](#f-98Gmc)s are defined in files under [[sym:./src/Symfony/Component/Form/Extension/Core/Type({"type":"path","text":"src/Symfony/Component/Form/Extension/Core/Type","path":"src/Symfony/Component/Form/Extension/Core/Type"})]].

<br/>

We first need to define our class in the relevant file, and inherit from `AbstractType`[<sup id="98Gmc">↓</sup>](#f-98Gmc):
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php
```hack
⬜ 14     use Symfony\Component\Form\AbstractType;
⬜ 15     use Symfony\Component\OptionsResolver\OptionsResolver;
⬜ 16     
🟩 17     class HiddenType extends AbstractType
⬜ 18     {
⬜ 19         /**
⬜ 20          * {@inheritdoc}
```

<br/>

> **Note**: the class name should end with "Type".

<br/>

### 2\. Implement configureOptions and getBlockPrefix

<br/>

The goal of `configureOptions`[<sup id="fbhew">↓</sup>](#f-fbhew) is to {Explain configureOptions's role}.

<br/>

In this example, `HiddenType`[<sup id="ZI92jX">↓</sup>](#f-ZI92jX), we {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php
```hack
⬜ 19         /**
⬜ 20          * {@inheritdoc}
⬜ 21          */
🟩 22         public function configureOptions(OptionsResolver $resolver)
⬜ 23         {
⬜ 24             $resolver->setDefaults([
⬜ 25                 // hidden fields cannot have a required attribute
```

<br/>

The goal of `getBlockPrefix`[<sup id="Z1pr0ud">↓</sup>](#f-Z1pr0ud) is to {Explain getBlockPrefix's role}.

<br/>

In this example, `HiddenType`[<sup id="ZI92jX">↓</sup>](#f-ZI92jX), we {Explain what's happening in this implementation}
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php
```hack
⬜ 34         /**
⬜ 35          * {@inheritdoc}
⬜ 36          */
🟩 37         public function getBlockPrefix(): string
⬜ 38         {
⬜ 39             return 'hidden';
⬜ 40         }
```

<br/>

## Update [[sym:./src/Symfony/Component/Form/Extension/Core/CoreExtension.php({"type":"path","text":"src/Symfony/Component/Form/Extension/Core/CoreExtension.php","path":"src/Symfony/Component/Form/Extension/Core/CoreExtension.php"})]]
Every time we add a new `AbstractType`[<sup id="98Gmc">↓</sup>](#f-98Gmc), we reference it in [[sym:./src/Symfony/Component/Form/Extension/Core/CoreExtension.php({"type":"path","text":"src/Symfony/Component/Form/Extension/Core/CoreExtension.php","path":"src/Symfony/Component/Form/Extension/Core/CoreExtension.php"})]].
We will still look at `HiddenType`[<sup id="ZI92jX">↓</sup>](#f-ZI92jX) as our example.

<br/>


<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Extension/Core/CoreExtension.php
```hack
⬜ 52                 new Type\DateType(),
⬜ 53                 new Type\DateTimeType(),
⬜ 54                 new Type\EmailType(),
🟩 55                 new Type\HiddenType(),
⬜ 56                 new Type\IntegerType(),
⬜ 57                 new Type\LanguageType(),
⬜ 58                 new Type\LocaleType(),
```

<br/>

## Optionally, these snippets may be helpful

<br/>

Update [[sym:./src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php({"type":"path","text":"src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php","path":"src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php"})]]
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php
```hack
⬜ 118                            return new TypeGuess(CollectionType::class, [], Guess::MEDIUM_CONFIDENCE);
⬜ 119                        case 'boolean':
⬜ 120                        case 'bool':
🟩 121                            return new TypeGuess(CheckboxType::class, [], Guess::MEDIUM_CONFIDENCE);
⬜ 122    
⬜ 123                        case 'double':
⬜ 124                        case 'float':
```

<br/>

Update [[sym:./src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php({"type":"path","text":"src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php","path":"src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php"})]]
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Extension/Validator/ValidatorTypeGuesser.php
```hack
⬜ 191    
⬜ 192                case IsTrue::class:
⬜ 193                case IsFalse::class:
🟩 194                    return new TypeGuess(CheckboxType::class, [], Guess::MEDIUM_CONFIDENCE);
⬜ 195            }
⬜ 196    
⬜ 197            return null;
```

<br/>

Update [[sym:./src/Symfony/Bridge/Doctrine/Form/DoctrineOrmTypeGuesser.php({"type":"path","text":"src/Symfony/Bridge/Doctrine/Form/DoctrineOrmTypeGuesser.php","path":"src/Symfony/Bridge/Doctrine/Form/DoctrineOrmTypeGuesser.php"})]]
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Bridge/Doctrine/Form/DoctrineOrmTypeGuesser.php
```hack
⬜ 65             return match ($metadata->getTypeOfField($property)) {
⬜ 66                 Types::ARRAY,
⬜ 67                 Types::SIMPLE_ARRAY => new TypeGuess(CollectionType::class, [], Guess::MEDIUM_CONFIDENCE),
🟩 68                 Types::BOOLEAN => new TypeGuess(CheckboxType::class, [], Guess::HIGH_CONFIDENCE),
⬜ 69                 Types::DATETIME_MUTABLE,
⬜ 70                 Types::DATETIMETZ_MUTABLE,
⬜ 71                 'vardatetime' => new TypeGuess(DateTimeType::class, [], Guess::HIGH_CONFIDENCE),
```

<br/>

Update [[sym:./src/Symfony/Component/Form/Extension/Core/Type/DateIntervalType.php({"type":"path","text":"src/Symfony/Component/Form/Extension/Core/Type/DateIntervalType.php","path":"src/Symfony/Component/Form/Extension/Core/Type/DateIntervalType.php"})]]
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Extension/Core/Type/DateIntervalType.php
```hack
⬜ 124                    }
⬜ 125                }
⬜ 126                if ($options['with_invert']) {
🟩 127                    $builder->add('invert', CheckboxType::class, [
⬜ 128                        'label' => $options['labels']['invert'],
⬜ 129                        'error_bubbling' => true,
⬜ 130                        'required' => false,
```

<br/>

Update [[sym:./src/Symfony/Bundle/FrameworkBundle/Resources/config/form.php({"type":"path","text":"src/Symfony/Bundle/FrameworkBundle/Resources/config/form.php","path":"src/Symfony/Bundle/FrameworkBundle/Resources/config/form.php"})]]
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Bundle/FrameworkBundle/Resources/config/form.php
```hack
⬜ 94                 ->args([service('form.property_accessor')])
⬜ 95                 ->tag('form.type')
⬜ 96     
🟩 97             ->set('form.type.choice', ChoiceType::class)
⬜ 98                 ->args([
⬜ 99                     service('form.choice_list_factory'),
⬜ 100                    service('translator')->ignoreOnInvalid(),
```

<br/>

Update [[sym:./src/Symfony/Component/Form/Forms.php({"type":"path","text":"src/Symfony/Component/Form/Forms.php","path":"src/Symfony/Component/Form/Forms.php"})]]
<!-- NOTE-swimm-snippet: the lines below link your snippet to Swimm -->
### 📄 src/Symfony/Component/Form/Forms.php
```hack
⬜ 24      *         ->add('firstName', 'Symfony\Component\Form\Extension\Core\Type\TextType')
⬜ 25      *         ->add('lastName', 'Symfony\Component\Form\Extension\Core\Type\TextType')
⬜ 26      *         ->add('age', 'Symfony\Component\Form\Extension\Core\Type\IntegerType')
🟩 27      *         ->add('color', 'Symfony\Component\Form\Extension\Core\Type\ChoiceType', [
⬜ 28      *             'choices' => ['Red' => 'r', 'Blue' => 'b'],
⬜ 29      *         ])
⬜ 30      *         ->getForm();
```

<br/>

<!-- THIS IS AN AUTOGENERATED SECTION. DO NOT EDIT THIS SECTION DIRECTLY -->
### Swimm Note

<span id="f-98Gmc">AbstractType</span>[^](#98Gmc) - "src/Symfony/Component/Form/AbstractType.php" L21
```hack
abstract class AbstractType implements FormTypeInterface
```

<span id="f-2plHN2">ChoiceType</span>[^](#2plHN2) - "src/Symfony/Component/Form/Extension/Core/Type/ChoiceType.php" L50
```hack
class ChoiceType extends AbstractType
```

<span id="f-fbhew">configureOptions</span>[^](#fbhew) - "src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php" L22
```hack
    public function configureOptions(OptionsResolver $resolver)
```

<span id="f-OosCu">DateType</span>[^](#OosCu) - "src/Symfony/Component/Form/Extension/Core/Type/DateType.php" L29
```hack
class DateType extends AbstractType
```

<span id="f-ENskR">FormType</span>[^](#ENskR) - "src/Symfony/Component/Form/Extension/Core/Type/FormType.php" L29
```hack
class FormType extends BaseType
```

<span id="f-Z1pr0ud">getBlockPrefix</span>[^](#Z1pr0ud) - "src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php" L37
```hack
    public function getBlockPrefix(): string
```

<span id="f-ZI92jX">HiddenType</span>[^](#ZI92jX) - "src/Symfony/Component/Form/Extension/Core/Type/HiddenType.php" L17
```hack
class HiddenType extends AbstractType
```

<span id="f-Zmiw25">TextType</span>[^](#Zmiw25) - "src/Symfony/Component/Form/Extension/Core/Type/TextType.php" L19
```hack
class TextType extends AbstractType implements DataTransformerInterface
```

<br/>

This file was generated by Swimm. [Click here to view it in the app](https://swimm-web-app--cu-2k0pfxz-hotfix-081-yya0h5n9.web.app/repos/Z2l0aHViJTNBJTNBc3ltZm9ueSUzQSUzQWlkb2dhbnplcg==/docs/ypo3a).