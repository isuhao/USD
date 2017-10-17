set(PXR_PREFIX pxr/usdImaging)
set(PXR_PACKAGE usdviewq)

if (NOT PXR_ENABLE_PYTHON_SUPPORT)
    message(STATUS "Not building testUsdview because PXR_ENABLE_PYTHON_SUPPORT=OFF")
    return()
elseif (NOT TARGET usdviewq)
    message(WARNING "Not building testUsdview because of missing dependency: usdviewq")
    return()
endif()

pxr_python_bin(testusdview
    DEPENDENCIES
        usdviewq
)

if (NOT PXR_HEADLESS_TEST_MODE)
    pxr_install_test_dir(
        SRC testenv/testUsdviewWrapper
        DEST testusdviewWrapper1
    )

    pxr_install_test_dir(
        SRC testenv/testUsdviewWrapper
        DEST testusdviewWrapper2
    )

    pxr_install_test_dir(
        SRC testenv/testUsdviewWrapper
        DEST testusdviewWrapper3
    )

    pxr_install_test_dir(
        SRC testenv/testUsdviewWrapper
        DEST testusdviewWrapper4
    )

    pxr_install_test_dir(
        SRC testenv/testUsdviewWrapper
        DEST testusdviewWrapper5
    )

    pxr_install_test_dir(
        SRC testenv/testUsdviewPrimPathBar
        DEST testusdviewPrimPathBar
    )

    pxr_register_test(testusdviewWrapper1
        PYTHON
        COMMAND "${CMAKE_INSTALL_PREFIX}/bin/testusdview --testScript testCallback.py"
        EXPECTED_RETURN_CODE 2
    )

    pxr_register_test(testusdviewWrapper2
        PYTHON
        COMMAND "${CMAKE_INSTALL_PREFIX}/bin/testusdview --testScript testCallback_Invalid_1.py test.usda"
        EXPECTED_RETURN_CODE 1
    )

    pxr_register_test(testusdviewWrapper3
        PYTHON
        COMMAND "${CMAKE_INSTALL_PREFIX}/bin/testusdview --testScript testCallback_Invalid_2.py test.usda"
        EXPECTED_RETURN_CODE 1
    )

    pxr_register_test(testusdviewWrapper4
        PYTHON
        COMMAND "${CMAKE_INSTALL_PREFIX}/bin/testusdview --testScript testCallback_Invalid_3.py test.usda"
        EXPECTED_RETURN_CODE 1
    )

    pxr_register_test(testusdviewWrapper5
        PYTHON
        COMMAND "${CMAKE_INSTALL_PREFIX}/bin/testusdview test.usda"
        EXPECTED_RETURN_CODE 2
    )

    pxr_register_test(testusdviewPrimPathBar
        PYTHON
        COMMAND "${CMAKE_INSTALL_PREFIX}/bin/testusdview --testScript testUsdviewPrimPathBar.py test.usda"
        EXPECTED_RETURN_CODE 0
    )
endif()