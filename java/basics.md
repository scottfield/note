### how to read file from classpath
    // From ClassLoader, all paths are "absolute" already - there's no context
    // from which they could be relative. Therefore you don't need a leading slash.
    InputStream in = this.getClass().getClassLoader()
    .getResourceAsStream("SomeTextFile.txt");
    // From Class, the path is relative to the package of the class unless
    // you include a leading slash, so if you don't want to use the current
    // package, include a slash like this:
    InputStream in = this.getClass().getResourceAsStream("/SomeTextFile.txt");
