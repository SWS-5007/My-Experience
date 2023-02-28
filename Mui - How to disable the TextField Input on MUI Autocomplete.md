# Mui - How to disable the TextField Input on MUI Autocomplete?

> Codebase
```
 <Autocomplete
    disablePortal
    id={id}
    options={OptionData}
    shrink={false}
    renderInput={({ inputProps, ...params }) => (
      <TextField
        {...params}
        placeholder="PlaceHolderText"
        label=""
        inputProps={{ ...inputProps, readOnly: true }}
      />
    )}
    size="small"
  />
```

This works well for me.
:-)