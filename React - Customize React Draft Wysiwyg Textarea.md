# React - Customize React Draft Wysiwyg Textarea?

> Note
Here is the Wysiwyg Textarea Doc and Demo.
https://jpuri.github.io/react-draft-wysiwyg/#/
https://dev.to/ebereplenty/react-textarea-with-editor-functionalities-427e

Please check these links first, and then review the codebase below.

> Codebase
```
import React, { useState, useEffect } from "react";
import { Box, Typography, useTheme } from "@mui/material";

import {
  EditorState,
  convertToRaw,
  convertFromHTML,
  ContentState,
} from "draft-js";
import { Editor } from "react-draft-wysiwyg";
import draftToHtml from "draftjs-to-html";
import htmlToDraft from "html-to-draftjs";
import "react-draft-wysiwyg/dist/react-draft-wysiwyg.css";

import "./styles.css";
const customToolbar = {
  options: [
    "inline",
    "blockType",
    "fontSize",
    "fontFamily",
    "list",
    "textAlign",
    // "colorPicker",
    // "link",
    // "embedded",
    // "emoji",
    // "image",
    // "remove",
    // "history",
  ],
  inline: {
    options: [
      "bold",
      "italic",
      "underline",
      // "strikethrough",
      // "monospace",
      // "superscript",
      // "subscript",
    ],
    // className: "custom-inline-toolbar",
    style: { fontSize: "10px", height: "10px" },
  },
  blockType: {
    options: [
      "Normal",
      "H1",
      "H2",
      "H3",
      "H4",
      "H5",
      "H6",
      "Blockquote",
      "Code",
    ],
  },
  fontSize: {
    options: [12, 14, 16, 18, 20, 24, 28, 32, 36, 40],
  },
  fontFamily: {
    options: [
      "Arial",
      "Georgia",
      "Impact",
      "Tahoma",
      "Times New Roman",
      "Verdana",
    ],
  },
  list: {
    options: ["unordered", "ordered"],
  },
  textAlign: {
    options: ["left", "center", "right", "justify"],
  },
};

const defaultValue = "<p>This is <strong>Defaultvalue</strong> .</p>";

export const Component = () => {
  const theme = useTheme();

  const [editorState, setEditorState] = useState(EditorState.createEmpty());

  useEffect(() => {
    //Getting content for defaultvalue of Editor from HTML Content
    const blocksFromHTML = convertFromHTML(defaultValue);
    const contentState = ContentState.createFromBlockArray(
      blocksFromHTML.contentBlocks,
      blocksFromHTML.entityMap
    );

    const editorState = EditorState.createWithContent(contentState);
    setEditorState(editorState);
  }, []);

  const [editorHtmlContent, setEditorHtmlContent] = useState();

  const onEditorStateChange = (state) => {
    setEditorState(state);

    //Getting HTML Content
    const htmlContent = draftToHtml(convertToRaw(state.getCurrentContent()));
    setEditorHtmlContent(htmlContent);
  };

  return (
    <>
      <Box>
        <Editor
          // readOnly={true}
          // toolbarHidden={true}      //Hide the Toolbar Box
          toolbar={customToolbar}     //Modify the Tools List of Toolbar
          editorState={editorState}     //Default Value
          onEditorStateChange={onEditorStateChange}   //Onchange Function
          wrapperClassName="demo-wrapper"    //Wrapper ClassName
          editorClassName="demo-editor"
          wrapperStyle={{ border: theme.border.main }}
          toolbarStyle={{ border: "none" }}
          editorStyle={{
            color: theme.palette.default,
            paddingLeft: "10px",
            paddingRight: "10px",
            fontSize: "15px",
          }}
        />
      </Box>
    </>
  );
};

```

This works well for me.
:-)