#include "common.hpp"

/* g_SecureBootPolicyBlobHeader 
	XREF Signature #1 @ A6F8B3: 0F 11 05 ? ? ? ? F2 0F 10 4F ? F2 0F 11 0D ? ? ? ? 44 39 77
*/

// 	SharedUserData->DbgSecureBootEnabled
// Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecureBoot\State
// Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecureBoot\Servicing\DeviceAttributes has some sys information

struct securebootpolicy {
	__int32 field_0;
	__int32 flags;
};

typedef struct _SYSTEM_SECUREBOOT_INFORMATION {
	bool secure_boot_enabled;
	bool secure_boot_capable;
} SYSTEM_SECUREBOOT_INFORMATION, * PSYSTEM_SECUREBOOT_INFORMATION;

/* char* g_SecureBootActivePlatformManifest 
	XREF Signature #1 @ A892F4: 48 89 2D ? ? ? ? 85 DB
	XREF Signature #2 @ 80BE40: 4C 8B 15 ? ? ? ? 4D 85 D2 75
	XREF Signature #3 @ 923066: 48 8B 15 ? ? ? ? 48 85 D2 75 ? B8

&& uint32_t g_SecureBootActivePlatformManifestSize 
	XREF Signature #1 @ 80BE56: 8B 0D ? ? ? ? 8D 41 ? 41 89 01
	XREF Signature #2 @ A892EE: 89 05 ? ? ? ? 48 89 2D ? ? ? ? 85 DB
*/
typedef struct _SYSTEM_SECUREBOOT_PLATFORM_MANIFEST_INFORMATION {
	uint32_t platform_manifest_size;
	unsigned char platform_manifest[1];
} SYSTEM_SECUREBOOT_PLATFORM_MANIFEST_INFORMATION, * PSYSTEM_SECUREBOOT_PLATFORM_MANIFEST_INFORMATION;

/* qword_CF4158 - SeSecureBootQueryInformation
	XREF Signature #1 @ 922D88: 48 39 1D ? ? ? ? 75 ? BF
	XREF Signature #2 @ A89316: 4C 89 35 ? ? ? ? 4C 8B CE
	XREF Signature #3 @ 922F29: 48 8B 05 ? ? ? ? 44 0F B7 50
	XREF Signature #4 @ A89200: 48 89 2D ? ? ? ? 66 44 39 73
	XREF Signature #5 @ 92326D: 48 8B 15 ? ? ? ? 33 C0 44 8B E6
*/

typedef struct _SYSTEM_SECUREBOOT_POLICY_INFORMATION {
	GUID policy_publisher;
	uint32_t policy_version;
	uint32_t policy_options;
} SYSTEM_SECUREBOOT_POLICY_INFORMATION, * PSYSTEM_SECUREBOOT_POLICY_INFORMATION;

typedef struct _SYSTEM_SECUREBOOT_POLICY_FULL_INFORMATION {
	SYSTEM_SECUREBOOT_POLICY_INFORMATION policy_information;
	uint32_t policy_size;
	unsigned char policy[1];
} SYSTEM_SECUREBOOT_POLICY_FULL_INFORMATION, * PSYSTEM_SECUREBOOT_POLICY_FULL_INFORMATION;

struct secure_boot_policy {
	char pad_0x4_0[0x4];
	GUID policy_publisher;
	unsigned __int32 policy_version;
	char pad_0x8_0[0x8];
	unsigned __int32 policy_options;
	char pad_0x14_0[0x14];
	unsigned __int32 policy_size;
	char policy[1];
};

NTSTATUS FxDriverEntry(PDRIVER_OBJECT driver_object, PUNICODE_STRING registry_path) {
	return STATUS_SUCCESS;
}
