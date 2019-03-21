.. README.rst
.. Copyright (c) 2013-2019 Pablo Acosta-Serafini
.. See LICENSE for details

.. [[[cog
.. # Standard library imports
.. import os
.. import sys
.. import textwrap
.. # PyPI imports
.. import pmisc
.. import docs.support.requirements_to_rst
.. SDIR = os.path.dirname(os.path.dirname(os.path.abspath(cog.inFile)))
.. sys.path.append(SDIR)
.. import pypkg.functions
.. FILE_NAME = sys.modules['docs.support.requirements_to_rst'].__file__
.. MDIR = os.path.join(os.path.realpath(
..    os.path.dirname(os.path.dirname(os.path.dirname(FILE_NAME))))
.. )
.. PKG_NAME = pypkg.functions.get_pkg_name()
.. PKG_VER = pypkg.functions.get_pkg_version()
.. PKG_INTERPS = pypkg.functions.get_supported_interps()
.. PKG_LONG_DESC = pypkg.functions.get_pkg_long_desc()
.. PKG_PIPELINE_ID = str(pypkg.functions.get_pkg_pipeline_id())
.. LINE_LENGTH = 78
.. PKG_INTERPS_STR = str(PKG_INTERPS[0]) if len(PKG_INTERPS) == 1 else ", ".join(PKG_INTERPS[:-1])+ " and " + PKG_INTERPS[-1]
.. def wrap(text, hanging_indent=0):
..     for line in textwrap.wrap(text, width=LINE_LENGTH, subsequent_indent=' '*hanging_indent):
..         cog.outl(line)
.. def tox_targets(prefix):
..     interps = ["``py"+str(interp).replace(".", "")+"-"+prefix+"``" for interp in PKG_INTERPS]
..     return interps[0] if len(interps) == 1 else ", ".join(interps[:-1])+ " and " + interps[-1]
.. cog.outl("")
.. cog.outl(".. image:: https://badge.fury.io/py/"+PKG_NAME+".svg")
.. cog.outl("    :target: https://pypi.org/project/"+PKG_NAME+"")
.. cog.outl("    :alt: PyPI version")
.. cog.outl("")
.. cog.outl(".. image:: https://img.shields.io/pypi/l/"+PKG_NAME+".svg")
.. cog.outl("    :target: https://pypi.org/project/"+PKG_NAME+"")
.. cog.outl("    :alt: License")
.. cog.outl("")
.. cog.outl(".. image:: https://img.shields.io/pypi/pyversions/"+PKG_NAME+".svg")
.. cog.outl("    :target: https://pypi.org/project/"+PKG_NAME+"")
.. cog.outl("    :alt: Python versions supported")
.. cog.outl("")
.. cog.outl(".. image:: https://img.shields.io/pypi/format/"+PKG_NAME+".svg")
.. cog.outl("    :target: https://pypi.org/project/"+PKG_NAME+"")
.. cog.outl("    :alt: Format")
.. cog.outl("")
.. cog.outl("|")
.. cog.outl("")
.. cog.outl(".. image::")
.. cog.outl("    https://dev.azure.com/pmasdev/"+PKG_NAME+"/_apis/build/status/pmacosta."+PKG_NAME+"?branchName=master")
.. cog.outl("    :target: https://dev.azure.com/pmasdev/"+PKG_NAME+"/_build?definitionId="+PKG_PIPELINE_ID+"&_a=summary")
.. cog.outl("    :alt: Continuous integration test status")
.. cog.outl("")
.. cog.outl(".. image::")
.. cog.outl("    https://img.shields.io/azure-devops/coverage/pmasdev/"+PKG_NAME+"/"+PKG_PIPELINE_ID+".svg")
.. cog.outl("    :target: https://dev.azure.com/pmasdev/"+PKG_NAME+"/_build?definitionId="+PKG_PIPELINE_ID+"&_a=summary")
.. cog.outl("    :alt: Continuous integration test coverage")
.. cog.outl("")
.. cog.outl(".. image::")
.. cog.outl("    https://readthedocs.org/projects/pip/badge/?version=stable")
.. cog.outl("    :target: https://pip.readthedocs.io/en/stable/?badge=stable")
.. cog.outl("    :alt: Documentation status")
.. cog.outl("")
.. cog.outl("|")
.. cog.outl("")
.. cog.outl("Description")
.. cog.outl("===========")
.. cog.outl("")
.. cog.outl(".. role:: bash(code)")
.. cog.outl("	:language: bash")
.. cog.outl("")
.. docs.support.requirements_to_rst.def_links(cog)
.. cog.outl("")
.. cog.outl("")
.. for paragraph in PKG_LONG_DESC.split(os.linesep):
..     wrap(paragraph)
..     cog.outl("")
.. cog.outl("Interpreter")
.. cog.outl("===========")
.. cog.outl("")
.. blurb = (
..     "The package has been developed and tested with Python {0} "
..     "under Linux (Debian, Ubuntu), Apple macOS and Microsoft Windows"
.. )
.. wrap(blurb.format(PKG_INTERPS_STR))
.. cog.outl("")
.. cog.outl("Installing")
.. cog.outl("==========")
.. cog.outl("")
.. cog.outl(".. code-block:: console")
.. cog.outl("")
.. cog.outl("	$ pip install "+PKG_NAME)
.. cog.outl("")
.. cog.outl("Documentation")
.. cog.outl("=============")
.. cog.outl("")
.. wrap("Available at `Read the Docs <https://"+PKG_NAME+".readthedocs.io>`_")
.. cog.outl("")
.. cog.outl("Contributing")
.. cog.outl("============")
.. cog.outl("")
.. cog.outl("1. Abide by the adopted `code of conduct")
.. cog.outl("   <https://www.contributor-covenant.org/version/1/4/code-of-conduct>`_")
.. cog.outl("")
.. blurb = (
..     "2. Fork the `repository <https://github.com/pmacosta/"+PKG_NAME+">`_ from "
..     "GitHub and then clone personal copy [#f1]_:"
.. )
.. wrap(blurb, 3)
.. cog.outl("")
.. cog.outl("    .. code-block:: console")
.. cog.outl("")
.. cog.outl("        $ github_user=myname")
.. cog.outl("        $ git clone --recurse-submodules \\")
.. cog.outl("              https://github.com/\"${github_user}\"/"+PKG_NAME+".git")
.. cog.outl("        Cloning into '"+PKG_NAME+"'...")
.. cog.outl("        ...")
.. cog.outl("        $ cd "+PKG_NAME+" || exit 1")
.. cog.outl("        $ export "+PKG_NAME.upper()+"_DIR=${PWD}")
.. cog.outl("        $")
.. cog.outl("")
.. cog.outl("3. The package uses two sub-modules: a set of custom Pylint plugins to help with")
.. cog.outl("   some areas of code quality and consistency (under the ``pylint_plugins``")
.. cog.outl("   directory), and a lightweight package management framework (under the")
.. cog.outl("   ``pypkg`` directory). Additionally, the `pre-commit framework")
.. cog.outl("   <https://pre-commit.com/>`_ is used to perform various pre-commit code")
.. cog.outl("   quality and consistency checks. To enable the pre-commit hooks:")
.. cog.outl("")
.. cog.outl("    .. code-block:: console")
.. cog.outl("")
.. cog.outl("        $ cd \"${"+PKG_NAME.upper()+"_DIR}\" || exit 1")
.. cog.outl("        $ pre-commit install")
.. cog.outl("        pre-commit installed at .../"+PKG_NAME+"/.git/hooks/pre-commit")
.. cog.outl("        $")
.. cog.outl("")
.. cog.outl("4. Ensure that the Python interpreter can find the package modules")
.. cog.outl("   (update the :bash:`$PYTHONPATH` environment variable, or use")
.. cog.outl("   `sys.paths() <https://docs.python.org/3/library/sys.html#sys.path>`_,")
.. cog.outl("   etc.)")
.. cog.outl("")
.. cog.outl("   .. code-block:: console")
.. cog.outl("")
.. cog.outl("       $ export PYTHONPATH=${PYTHONPATH}:${"+PKG_NAME.upper()+"_DIR}")
.. cog.outl("       $")
.. cog.outl("")
.. cog.outl("5. Install the dependencies (if needed, done automatically by pip):")
.. docs.support.requirements_to_rst.proc_requirements(cog)
.. cog.outl("6. Implement a new feature or fix a bug")
.. cog.outl("")
.. cog.outl("7. Write a unit test which shows that the contributed code works as expected.")
.. cog.outl("   Run the package tests to ensure that the bug fix or new feature does not")
.. cog.outl("   have adverse side effects. If possible achieve 100\% code and branch")
.. cog.outl("   coverage of the contribution. Thorough package validation")
.. cog.outl("   can be done via Tox and Pytest:")
.. cog.outl("")
.. cog.outl("   .. code-block:: console")
.. cog.outl("")
.. cog.outl("       $ PKG_NAME="+PKG_NAME+" tox")
.. cog.outl("       GLOB sdist-make: .../"+PKG_NAME+"/setup.py")
.. cog.outl("       py27-pkg create: .../"+PKG_NAME+"/.tox/py27")
.. cog.outl("       py27-pkg installdeps: -r.../"+PKG_NAME+"/requirements/tests_py27.pip, -r.../"+PKG_NAME+"/requirements/docs_py27.pip")
.. cog.outl("       ...")
.. for pyver in PKG_INTERPS:
..     cog.outl("         py{0}-pkg: commands succeeded".format(str(pyver).replace(".", "")))
.. cog.outl("           congratulations :)")
.. cog.outl("       $")
.. cog.outl("")
.. cog.outl("   `Setuptools <https://bitbucket.org/pypa/setuptools>`_ can also be used")
.. cog.outl("   (Tox is configured as its virtual environment manager):")
.. cog.outl("")
.. cog.outl("   .. code-block:: console")
.. cog.outl("")
.. cog.outl("       $ PKG_NAME="+PKG_NAME+" python setup.py tests")
.. cog.outl("       running tests")
.. cog.outl("       running egg_info")
.. cog.outl("       writing "+PKG_NAME+".egg-info/PKG-INFO")
.. cog.outl("       writing dependency_links to "+PKG_NAME+".egg-info/dependency_links.txt")
.. cog.outl("       writing requirements to "+PKG_NAME+".egg-info/requires.txt")
.. cog.outl("       ...")
.. for pyver in PKG_INTERPS:
..     cog.outl("         py{0}-pkg: commands succeeded".format(str(pyver).replace(".", "")))
.. cog.outl("         congratulations :)")
.. cog.outl("       $")
.. cog.outl("")
.. blurb = (
..     "Tox (or Setuptools via Tox) runs with the following default environments: "+
..     tox_targets("pkg")+" [#f3]_. These use "+
..     "the "+PKG_INTERPS_STR+" interpreters, respectively, to test all code in the "+
..     "documentation (both in Sphinx ``*.rst`` source files and in docstrings), run "+
..     "all unit tests, measure test coverage and re-build the exceptions "+
..     "documentation. To pass arguments to Pytest (the test runner) use a double "+
..     "dash (``--``) after all the Tox arguments, for example:"
.. )
.. wrap((" "*3)+blurb, hanging_indent=3)
.. cog.outl("")
.. cog.outl("   .. code-block:: console")
.. cog.outl("")
.. cog.outl("       $ PKG_NAME="+PKG_NAME+" tox -e py27-pkg -- -n 4")
.. cog.outl("       GLOB sdist-make: .../"+PKG_NAME+"/setup.py")
.. cog.outl("       py27-pkg inst-nodeps: .../"+PKG_NAME+"/.tox/.tmp/package/1/"+PKG_NAME+"-"+PKG_VER+".zip")
.. cog.outl("       ...")
.. cog.outl("         py27-pkg: commands succeeded")
.. cog.outl("         congratulations :)")
.. cog.outl("       $")
.. cog.outl("")
.. cog.outl("   Or use the :code:`-a` Setuptools optional argument followed by a quoted")
.. cog.outl("   string with the arguments for Pytest. For example:")
.. cog.outl("")
.. cog.outl("   .. code-block:: console")
.. cog.outl("")
.. cog.outl("       $ PKG_NAME="+PKG_NAME+" python setup.py tests -a \"-e py27-pkg -- -n 4\"")
.. cog.outl("       running tests")
.. cog.outl("       ...")
.. cog.outl("         py27-pkg: commands succeeded")
.. cog.outl("         congratulations :)")
.. cog.outl("       $")
.. cog.outl("")
.. cog.outl("   There are other convenience environments defined for Tox [#f3]_:")
.. cog.outl("")
.. blurb = (
..     "* "+tox_targets("repl")+" run the Python "+PKG_INTERPS_STR+" "+
..     "REPL, respectively, in the appropriate virtual "+
..     "environment. The ``"+PKG_NAME+"`` package is pip-installed by Tox when the "+
..     "environments are created.  Arguments to the interpreter can be passed in "+
..     "the command line after a double dash (``--``)."
.. )
.. wrap((" "*4)+blurb, hanging_indent=6)
.. cog.outl("")
.. blurb = (
..     "* "+tox_targets("test")+" run Pytest "+
..     "using the Python "+PKG_INTERPS_STR+" interpreter, "+
..     "respectively, in the appropriate virtual environment. Arguments to pytest "+
..     "can be passed in the command line after a double dash (``--``) , for "+
..     "example:"
.. )
.. wrap((" "*4)+blurb, hanging_indent=6)
.. cog.outl("")
.. cog.outl("      .. code-block:: console")
.. cog.outl("")
.. cog.outl("          $ PKG_NAME="+PKG_NAME+" tox -e py27-test -- -x test_"+PKG_NAME+".py")
.. cog.outl("       GLOB sdist-make: .../"+PKG_NAME+"/setup.py")
.. cog.outl("       py27-pkg inst-nodeps: .../"+PKG_NAME+"/.tox/.tmp/package/1/"+PKG_NAME+"-"+PKG_VER+".zip")
.. cog.outl("       ...")
.. cog.outl("         py27-pkg: commands succeeded")
.. cog.outl("         congratulations :)")
.. cog.outl("       $")
.. PY_LIST = "``"+str(PKG_INTERPS[0])+"``" if len(PKG_INTERPS) == 1 else ", ".join(["``"+str(item)+"``" for item in PKG_INTERPS[:-1]])+" or ``"+str(PKG_INTERPS[-1])+"``"
.. blurb = (
..     "* "+tox_targets("test")+" test code and "+
..     "branch coverage using the "+PKG_INTERPS_STR+" interpreter, respectively, "+
..     "in the appropriate virtual environment. Arguments to pytest can be passed "+
..     "in the command line after a double dash (``--``). The report can be found "+
..     "in "+
..     ":bash:`${"+PKG_NAME.upper()+"_DIR}/.tox/py[PV]/usr/share/"+PKG_NAME+"/tests/htmlcov/index.html` "+
..     "where ``[PV]`` stands for "+PY_LIST+" depending on "+
..     "the interpreter used."
.. )
.. wrap((" "*4)+blurb, hanging_indent=6)
.. cog.outl("")
.. cog.outl("8. Verify that continuous integration tests pass. The package has continuous")
.. cog.outl("   integration configured for Linux, Apple macOS and Microsoft Windows (all via")
.. cog.outl("   `Azure DevOps <https://dev.azure.com/pmasdev>`_).")
.. cog.outl("")
.. cog.outl("9. Document the new feature or bug fix (if needed). The script")
.. cog.outl("   :bash:`${"+PKG_NAME.upper()+"_DIR}/pypkg/build_docs.py` re-builds the whole package")
.. cog.outl("   documentation (re-generates images, cogs source files, etc.):")
.. cog.outl("")
.. pmisc.ste('"${'+PKG_NAME.upper()+'_DIR}"/pypkg/build_docs.py -h', 3, MDIR, cog.out, env={PKG_NAME.upper()+"_DIR":MDIR})
.. cog.outl(".. rubric:: Footnotes")
.. cog.outl("")
.. cog.outl(".. [#f1] All examples are for the `bash <https://www.gnu.org/software/bash/>`_")
.. cog.outl("   shell")
.. cog.outl("")
.. cog.outl(".. [#f2] It is assumed that all the Python interpreters are in the executables")
.. cog.outl("   path. Source code for the interpreters can be downloaded from Python's main")
.. cog.outl("   `site <https://www.python.org/downloads/>`_")
.. cog.outl("")
.. cog.outl(".. [#f3] Tox configuration largely inspired by")
.. cog.outl("   `Ionel's codelog <https://blog.ionelmc.ro/2015/04/14/")
.. cog.outl("   tox-tricks-and-patterns/>`_")
.. cog.outl("")
.. cog.outl(".. include:: ../CHANGELOG.rst")
.. cog.outl("")
.. cog.outl("License")
.. cog.outl("=======")
.. cog.outl("")
.. cog.outl(".. include:: ../LICENSE")
.. ]]]
.. [[[end]]]
