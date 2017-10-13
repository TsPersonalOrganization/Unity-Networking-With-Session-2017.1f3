# README #

The Unity Networking extension DLL is the open source component of the Unity Multiplayer Networking system. In this DLL we have the whole networking system except the NetworkTransport related APIs and classes. This is all the high level classes and components which make up the user friendly system of creating multiplayer games. This document details how you can compile your own version of the Networking extension DLL and use that in your games and applications.

### What license is the Networking extension DLL shipped under? ###
The Networking extension DLL is released under an MIT/X11 license; see the LICENSE file.

This means that you pretty much can customize and embed it in any software under any license without any other constraints than preserving the copyright and license information while adding your own copyright and license information.

You can keep the source to yourself or share your customized version under the same MIT license or a compatible license.

If you want to contribute patches back, please keep it under the unmodified MIT license so it can be integrated in future versions and shared under the same license.

### How do I get started? ###
* Clone this repository onto a location on your computer.
* Configure your IDE for the Unity coding standard, look in the .editorconfig file for more information
* Open the project in Visual Studio or MonoDevelop
    * If you are using MonoDevelop
        * Ensure you enable XBuild (Preferences -> Projects -> Build ->"Compile projects using MSBuild/XBuild")
        * You may need to restart MonoDevelop
    * Build the solution

* A folder will be created in the root directory called "Output", the generated dll's will output here in the correct folder structure
    * Windows: Copy the contents of Output folder to: `Data\UnityExtensions\Unity\Networking\{UNITY_VERSION}`
    * OSX: Copy the contents of Output folder to: `Unity.app/Contents/UnityExtensions/Unity/Networking/{UNITY_VERSION}`

* For the weaver the files need to be copied to a different place, they appear in "Output/Weaver"
    * Windows: Copy the contents of Output/Weaver folder to: `Data\Managed`
    * OSX: Copy the contents of Output/Weaver folder to: `Unity.app/Contents\Managed`

* If you want the dll's to copy automatically on build
    * For each visual studio project file
        * Open the file in a text editor
        * Locate the section: <Target Name="AfterBuild">
        * Follow the instructions in the comments

### Will you be taking pull requests? ###
We'll consider all incoming pull requests that we get. It's likely we'll take bug fixes this way but anything else will be handled on a case by case basis. Changes will not be applied directly to this repository but to the mainline Unity repository and will then appear here when the code is released in a new Unity version.


//###################2017.09.19

1.在NetworkConnection类，增加groupId字段，默认值为0；
2.在NetworkConnection类，增加SetGroupId方法，作用为给groupId字段赋值；
3.在NetworkIdentity类，增加了groupId属性，当NetworkIdentity在生成的时候，有被赋值过groupId时，则获取该groupId,否则，当有Owner的时候，返回Owner的groupID,否则返回0；
4.NetworkServer.SndWriterToReady方法增加groupID参数 ，默认为0；
5.NetworkServer.SendBytesToReady方法增加groupID参数 ，默认为0；
6.NetworkServer.SetClientReadyInternal 方法中，AddObserver时，只add groupId一致的conn
7.NetworkServer.SpawnObject方法增加groupID参数 ，默认为0；
8.NetworkServer.Spawn方法增加groupID参数 ，默认为0；
9.NetworkIdentity.RebuildObservers方法增加groupID参数，默认为0;
10.增加了SpawnExDelegate(Vector3 position, NetworkHash128 assetId, string data); 以便在Spawn的时候传送其它数据
11.ClientScene增加了 SpawnExDelegate相关的RegisterPrefab,RegisterSpawnHandler方法。
12.NetworkScene增加了 存储SpawnExDelegate的相关Hashtable字段：s_SpawnExHandlers，并在获取,移除,清空Spawner时针对s_SpawnExHandlers做了相应增加删除处理，。
13.NetworkScene增加了 SpawnExDelete相关的RegisterPrefab,RegisterSpawnHandler方法。
14.NetworkScene增加了 GetSpawnHandler(NetworkHash128 assetId, out SpawnExDelegate handler)，方法用于获取新的SpawnExDelegate
15.NetworkServer增加Spawn方法的data参数，默认为空。
16.NetworkServer增加SpawnObject方法的data参数，默认为空。


