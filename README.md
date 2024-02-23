# Expo image manipulator

Multi platform 🚀

[![npm version](https://badge.fury.io/js/expo-image-crop.svg)](https://github.com/brunon80/expo-image-crop)
[![platform-ios/android](https://img.shields.io/badge/platform-ios%2Fandroid-blue.svg)](https://github.com/brunon80/expo-image-crop)
[![license-MIT](https://img.shields.io/badge/license-MIT-lightgrey.svg)](https://github.com/brunon80/expo-image-crop)

<a href="https://exp.host/@koruja/expo-image-crop">Abra em seu dispositivo!</a>

[PRs são bem-vindos...](https://github.com/brunon80/expo-image-crop/pulls)

### Dependências do Expo
- yarn add react-native-vector-icons
- expo install expo-permissions
- expo install expo-image-picker
- expo install expo-file-system
- expo install expo-image-manipulator

## Exemplo

```javascript
import React from 'react'
import { Dimensions, Button, ImageBackground } from 'react-native'
import { ImageManipulator } from 'expo-image-crop'

export default class App extends React.Component {
  state = {
      isVisible: false,
      uri: 'https://i.pinimg.com/originals/39/42/a1/3942a180299d5b9587c2aa8e09d91ecf.jpg',
  }
  onToggleModal = () => {
      const { isVisible } = this.state
      this.setState({ isVisible: !isVisible })
  }
  render() {
      const { uri, isVisible } = this.state
      const { width, height } = Dimensions.get('window')
      return (
          <ImageBackground
              resizeMode="contain"
              style={{
                  justifyContent: 'center', padding: 20, alignItems: 'center', height, width, backgroundColor: 'black',
              }}
              source={{ uri }}
          >
              <Button title="Open Image Editor" onPress={() => this.setState({ isVisible: true })} />
              <ImageManipulator
                  photo={{ uri }}
                  isVisible={isVisible}
                  onPictureChoosed={({ uri: uriM }) => this.setState({ uri: uriM })}
                  onToggleModal={this.onToggleModal}
              />
          </ImageBackground>
      )
  }
}
```

## Props

| Props            | Tipo     | Padrão                                                                    | Descrição                                        |
|------------------|----------|----------------------------------------------------------------------------|----------------------------------------------------|
| isVisible        | boolean  | false                                                                      | Mostra ou oculta o modal com a UI de manipulação de imagem       |
| onPictureChoosed | função |                                                                            | Callback onde é passada a imagem editada como parâmetro |
| photo            | objeto   | ```{  "uri": string } ```                                       | uri da imagem a ser editada                          |
| btnTexts         | objeto   | ```{ "crop": string, "done": string, "processing": string}```    | nome para os textos de recorte, concluído e processamento           |
| onToggleModal    | função |                                                                            | Callback chamado quando o modal é fechado            |
| borderColor      | string   | #a4a4a4                                                                    | Cor da borda da máscara de recorte                         |
| allowRotate      | boolean  | true                                                                       | Mostra a opção de rotação                                 |
| allowFlip        | boolean  | true                                                                       | Mostra a opção de espelhamento                                   |
| saveOptions      | objeto   | ```{ "compress": number, "format": string, "base64": boolean}``` | Um mapa definindo como a imagem modificada deve ser salva  
| fixedMask      | objeto   | ```{ "width": number, "height": number }``` | Largura e altura da máscara fixa


## O retorno de onPictureChoosed é um objeto com o formato:

```javascript
{
    uri: string,
    base64: string // undefined se base64 for false na propriedade saveOptions
}
```
## Execute o exemplo!
- Clone este repositório
- cd example/
- execute yarn ou npm install
- aproveite!
### A animação é fluída mesmo no modo de desenvolvimento!


## Requisitos
* Use-o em um app Expo (do cliente expo, app autônomo ou app ExpoKit).
* Porque precisamos ter acesso ao `ImageManipulator`

## Funcionalidades
* Recorte
* Rotação
* Espelhamento (Horizontal e Vertical)
* Base64