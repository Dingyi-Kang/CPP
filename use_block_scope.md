If you did not create `_index` with `new`, it means that `_index` is a local object and its memory will be automatically managed by the scope it is in. However, if you want to free the memory used by `_index` as soon as you are done using it, you can use a block scope to limit the lifetime of the `_index` object. 

Here’s how you can ensure `_index` is destructed immediately after its use by enclosing it in a block scope:

```cpp
{
    // Define and initialize _index within a block scope
    diskann::Index<T, TagT, LabelT> _index(
        compareMetric, base_dim, base_num,
        std::make_shared<diskann::IndexWriteParameters>(paras), nullptr,
        defaults::NUM_FROZEN_POINTS_STATIC, false, false, false,
        build_pq_bytes > 0, build_pq_bytes, use_opq, use_filters
    );

    if (!use_filters)
    {
        _index.build(base_file.c_str(), base_num);
    }
    else
    {
        if (universal_label != "")
        {
            // Indicates no universal label
            LabelT unv_label_as_num = 0;
            _index.set_universal_label(unv_label_as_num);
        }
        _index.build_filtered_index(base_file.c_str(), label_file, base_num);
    }
    _index.save(mem_index_path.c_str());

    // _index will be destructed when it goes out of this scope
}

// Code after the block scope can run with _index already destructed
```

### Explanation
- **Block Scope**: By defining `_index` within a block scope `{ ... }`, you ensure that `_index` is destructed as soon as the block is exited.
- **Memory Management**: The destructor for `_index` will be called automatically when it goes out of scope, freeing the memory and resources used by `_index`.

### Example with Additional Code Following the Destruction
If you have other code that needs to run after `_index` has been destructed, it would look like this:

```cpp
{
    // Define and initialize _index within a block scope
    diskann::Index<T, TagT, LabelT> _index(
        compareMetric, base_dim, base_num,
        std::make_shared<diskann::IndexWriteParameters>(paras), nullptr,
        defaults::NUM_FROZEN_POINTS_STATIC, false, false, false,
        build_pq_bytes > 0, build_pq_bytes, use_opq, use_filters
    );

    if (!use_filters)
    {
        _index.build(base_file.c_str(), base_num);
    }
    else
    {
        if (universal_label != "")
        {
            // Indicates no universal label
            LabelT unv_label_as_num = 0;
            _index.set_universal_label(unv_label_as_num);
        }
        _index.build_filtered_index(base_file.c_str(), label_file, base_num);
    }
    _index.save(mem_index_path.c_str());

    // _index will be destructed when it goes out of this scope
}

// Additional code to run after _index is destructed
// ...
```

This approach ensures that `_index` is destructed as soon as it is no longer needed, freeing up the memory it used.
