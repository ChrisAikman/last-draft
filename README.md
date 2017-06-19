# [last-draft](http://lastdraft.xyz)

[![npm version](https://badge.fury.io/js/last-draft.svg)](https://badge.fury.io/js/last-draft)

[![Standard - JavaScript Style Guide](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

![](https://raw.githubusercontent.com/vacenz/last-draft/master/example/public/screenshot.gif)

[last-draft](http://lastdraft.xyz) is a Draft.js editor using [draft-js-plugins](https://draft-js-plugins.com)

## Important Note:

## Versions

#### `3.3.0` in progress version using [draft-js-plugins](https://draft-js-plugins.com) and [last-draft-js-plugins](https://github.com/vacenz/last-draft-js-plugins)

- [v3 docs](https://github.com/vacenz/last-draft/tree/v3)

- [v3 demo](http://lastdraft.xyz/v3)

- [v3 example repo](https://github.com/vacenz/last-draft-example-v3)

```jsx
yarn add last-draft
```

#### `2.3.3` stable version using [MegaDraft](https://github.com/globocom/megadraft) plugin approach and ld-plugins

- [v2 docs](https://github.com/vacenz/last-draft/tree/v2)

- [v2 demo](http://lastdraft.xyz)

- [v2 example-repo](https://github.com/vacenz/last-draft-example)

```jsx
yarn add last-draft@2.3.3
```

## v3 Use
```jsx
import React, { Component } from 'react'
import { render } from 'react-dom'
import {Editor, editorStateFromHtml, editorStateToHtml, editorStateFromRaw, editorStateFromText} from 'last-draft'
import { fromJS } from 'immutable';

export default class ExampleEditor extends Component {
  constructor(props) {
    super(props)
    const INITIAL_STATE = editorStateFromText('this is a cooel editor... 🏄🌠🏀')
    this.state = { editorState: INITIAL_STATE }
  }

  onChange = (editorState) => {
    this.setState({ editorState: editorState })
    /* You would normally save this to your database here instead of logging it */
    console.log(editorStateToHtml(editorState))
  }

  render() {
    return (
      <Editor
        editorState={this.state.editorState}
        placeholder='Text'
        onChange={::this.onChange} />
    )
  }
}
```

## v2 Use
```jsx
import React, { Component } from 'react'
import { render } from 'react-dom'
import {Editor, editorStateFromHtml, editorStateToHtml, editorStateFromRaw, editorStateToJSON} from 'last-draft'

import video from 'ld-video'
import color from 'ld-color-picker'
import emoji from 'ld-emoji'
import gif from 'ld-gif'
import mention from 'ld-mention'
import audio from 'ld-audio'
import sticker from 'ld-sticker'
import html from 'ld-html'
import todo from 'ld-todo'
let plugins = [video, color, emoji, gif, mention]

/* init the state, either from raw or html */
import raw from './initialState/raw'


export default class ExampleEditor extends Component {
  constructor(props) {
    super(props)
    const INITIAL_STATE = editorStateFromRaw(raw)
    this.state = { value: INITIAL_STATE }
  }

  onChange(editorState) {
    this.setState({ value: editorState })
    console.log(editorStateToHtml(editorState))
    console.log(editorStateToJSON(editorState))
  }

  render() {
    return (
      <Editor
        plugins={plugins}
        editorState={this.state.value}
        placeholder='Enter text...'
        onChange={::this.onChange} />
    )
  }
}
```
