[[Jest]]
[[Testes com Jest]]

`describe(name, fn)` cria um bloco que agrupa vários testes relacionados. Por exemplo, se você tiver um objeto `myBeverage` que deve ser delicioso, mas não azedo, você pode testá-lo com:

```js
const myBeverage = {
	delicious: true, 
	sour: false,
};

describe('my beverage', () => {
	test('is delicious', () => {
	    expect(myBeverage.delicious).toBeTruthy();  
	});
	
	test('is not sour', () => {
	    expect(myBeverage.sour).toBeFalsy();
	});
});
```

Isso não é necessário - você pode escrever os blocos de `teste` diretamente em nível superior. Mas isso pode ser útil se preferir que os seus testes sejam organizados em grupos.

Você também pode aninhar blocos `describe` se você tem uma hierarquia de testes:

```js
const binaryStringToNumber = binString => {
	if (!/^[01]+$/.test(binString)) {
	    throw new CustomError('Not a binary number.');
	}
	
	return parseInt(binString, 2);
};
describe('binaryStringToNumber', () => {
	describe('given an invalid binary string', () => {
	    test('composed of non-numbers throws CustomError', () => {
		    expect(() => binaryStringToNumber('abc')).toThrow(CustomError);
		});
		
		test('with extra whitespace throws CustomError', () => {
		      expect(() => binaryStringToNumber('  100')).toThrow(CustomError);
		});
	});
	describe('given a valid binary string', () => {
	    test('returns the correct number', () => {  
	        expect(binaryStringToNumber('100')).toBe(4);
	    });
	});
});
```
