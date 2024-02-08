If you define a template class that you only want to work for a couple of explicit types.

Put the template declaration in the header file just like a normal class.

Put the template definition in a source file just like a normal class.

Then, at the end of the source file, explicitly instantiate only the version you want to be available.