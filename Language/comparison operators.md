`<=, >=, <, >`
Something to note:

`seg_it->first <= *p_it <= seg_it->second` will not evaluate correctly. You need to write `seg_it->first <= *p_it && *p_it >= seg_it`

