---
title: Quickstart
heading: Start Using Xpect
layout: page
---


Get up and running quickly with the following example:


{: .spaced }

1. Install Xpect via methods described in the [Downloads Page](download)
2. Let's assume you hava an Xtext Language you want to test which uses the file extension `*.dmodel`. 
3. If you don't have such a language, get one in Eclipse via <kbd>File > New > Example > Xtext > Examples > Xtext Domain Model</kbd>
4. If you don't have the language installed, launch a runtime workbench where it is installed.
5. Create a new Plug-in Project and add  
    * `org.xpect.xtext.lib`
    * your languages runtime-project (the one with the grammar inside) 
    * your UI-project to the dependencies
6. Create a new Junit Test such as `package mytest`;

    ```java
    import org.junit.runner.RunWith;
    import org.xpect.runner.XpectRunner;
    import org.xpect.xtext.lib.tests.XtextTests;

    @RunWith(XpectRunner.class)
    public class MyXtextTests extends XtextTests {
    }
    ```
    The class `XtextTests` is a test suite with predefined tests that ships with Xpect.
7. Create a file `mytest.dmodel.xt` inside the same package as the test class.

    {: .alert .alert-success}
    Note that this file has two file extensions. The first one indicates your language and the second one is `.xt`.

    ```java
    /* XPECT_SETUP mytest.MyXtextTests END_SETUP */
    package pkg1 {
      entity MyEntity1 {
        
        // int should be the java primitive
        // XPECT linkedName at int --> int
        id:int
        
        // String should be from java.lang 
        // XPECT linkedName at String --> java.lang.String
        name:String
        
        // besides "int", we can reference... and we can not reference foooobar
        // XPECT scope at int --> int, String, java.lang.String, boolean, !foooobar, ...
        id:int
        
        // XPECT errors --> "Couldn't resolve reference to JvmType 'integer'." at "integer"
        id:integer
      }
    }
    ```


### Running

Now you can right-click on the file and choose <kbd>open</kbd> to reveal three editors:
* An Xpect+Xtext editor with highlighting, content assist, etc. for both your language and the Xpect syntax.
* An Xpect editor with support for the Xpect syntax.
* The editor for your language that you build.
Running the Java class as JUnit test executes the test cases specified in the `mytest.dmodel.xt` file.

If a test fails, double-clicking on it in the JUnit view opens a comparison editor which compares the test's expectation with the actual test result. 
This eases understanding why a test fails dramatically.

In the context menu of a test in the JUnit view, you can select go to XPECT to open and select test case in the DSL-File.
Find further examples for the Domainmodel Language here. 

