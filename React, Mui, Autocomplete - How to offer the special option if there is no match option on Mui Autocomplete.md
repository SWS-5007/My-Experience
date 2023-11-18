# React, Mui, Autocomplete - How to offer the special option if there is no match option on Mui Autocomplete?

> Example 1:

```
import { MenuItem, createFilterOptions } from '@mui/material';

const filter = createFilterOptions<any>();

<Autocomplete
  options={options}
  getOptionLabel={(option: any) => (option ? option.label : '')}
  value={value}
  autoComplete={false}
  onChange={handleSelect}
  inputValue={search}
  disabled={disabled}
  onInputChange={(_a, b) => handleSearch(b)}
  loading={loading}

//This property makes to offer speical option if there is no match option.
  filterOptions={(options: any, params: any) => {
    const filteredOptions = filter(options, params);
    const { inputValue } = params;
    const isExisting = options.some(
      (option: any) => inputValue === option.label
    );
    if (inputValue !== '' && !isExisting)
      filteredOptions.push({ label: 'Other', value: 15 });
    return filteredOptions;
  }}
  noOptionsText={noOptionsText}
  isOptionEqualToValue={(a: any, b: any) => a.value === b.value}
  renderOption={(optionProps, option: any) => (
    <MenuItem key={option.value} {...optionProps}>
      {option.label}
    </MenuItem>
  )}
  renderInput={({
    InputProps: { endAdornment: _endAdornment, ...InputProps },
    ...x
  }) => (
    <InputText
      {...x}
      variant="outlined"
      placeholder={placeholder}
      error={error}
      onBlur={handleBlur}
      onFocus={handleFocus}
      disabled={disabled}
      // onKeyDown={handleKeyDown}
      InputProps={{
        ...InputProps,
        startAdornment,
        endAdornment: [endAdornment, _endAdornment],
      }}
    />
  )}
/>

```

> Example 2:

```
import { MenuItem, createFilterOptions } from '@mui/material';

const filter = createFilterOptions<any>();

<Autocomplete
  className="col-span-full"
  required
  autocompleteProps={{
    freeSolo: true,
    placeholder: "Select Organization",
    options: organizations,
    value: organizations.find((org) => org.id === organization.id),
    filterOptions: (options, params) => {
      const filtered = filter(options, params);
      const { inputValue } = params;
      const isExisting = options.some((option) => inputValue === option.title);
      if (inputValue !== "" && !isExisting)
        filtered.push({ name: "Adding...", value: inputValue });
      return filtered;
    },
    getOptionLabel: (option) =>
      typeof option === "string" ? option : option.name,
    onChange: (event, value, reason, details) => {
      debounceOrganization(
        value?.name === "Adding..."
          ? {
              address1: "",
              address2: "",
              city: "",
              country: "",
              customUrl: "",
              description: "",
              employees: 0,
              hiringUrl: "",
              id: "",
              isHiring: false,
              logo: "",
              name: value?.value,
              url: "",
              website: "",
              year: "",
              zip: "",
            }
          : value
      );
    },
    renderOption: (props, option) => (
      <AutocompleteOption {...props}>
        <ListItemContent sx={{ color: "black", fontSize: "sm" }}>
          {option.name}
        </ListItemContent>
      </AutocompleteOption>
    ),
  }}
/>;

```
