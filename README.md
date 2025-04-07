# Secure Coding Examples

## 1. Assume Failure

```cpp
status_t AES_128_CBC_encrypt ( const byte* input, byte* output, const int len, const AES_KEY* key )
{
   status_t status = ERROR;

   // Do encryption
   // ...
   
   status = OK;
}
```

## 2. Redundancy

```cpp
status_t AES_128_CBC_encrypt ( const byte* input, byte* output, const int len, const AES_KEY* key )
{
   int i = 0;
   int verif = len;  

   for ( i = 0 ; i < len ; i++ )
   {
       // do something
       verif--;
   }

   if ( verif != 0 )
   {
       // Fault detected
   }
   else
   {
       // all good
   }
...
```

## 3. Constant Time Operations

#### Example 1
```cpp
status_t PINVerification ( const byte* submittedPIN, const byte* PIN )
{
   for ( int i = 0 ; i < 4 ; i++ )
   {
       if ( submittedPIN[i] != PIN[i])
           return REJECTED;
   }

   return ACCEPTED;
}
```


#### Example 2
```cpp
int secureCompare ( const byte *a, const byte *b, int len )
{
   int result = 0;

   for ( int i = 0 ; i < len ; i++ )
   {
       result |= a[i] ^ b[i];
   }

   return result;
}
```
